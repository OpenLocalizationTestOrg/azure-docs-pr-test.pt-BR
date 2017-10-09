---
title: "Grupos de disponibilidade de servidor - máquinas virtuais do Azure - Tutorial de aaaSQL | Microsoft Docs"
description: "Este tutorial mostra como toocreate um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configurar grupos de disponibilidade Sempre ativo na VM do Azure manualmente

Este tutorial mostra como toocreate um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure. tutorial completo Olá cria um grupo de disponibilidade com uma réplica de banco de dados em dois servidores SQL.

**Tempo estimado**: leva aproximadamente 30 minutos toocomplete depois Olá pré-requisitos forem atendidos.

diagrama de saudação ilustra o que você cria no tutorial de saudação.

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Pré-requisitos

tutorial de saudação pressupõe que você tem uma compreensão básica do SQL Server AlwaysOn em grupos de disponibilidade. Se você precisa saber mais, confira [Visão geral dos Grupos de Disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Olá tabela a seguir lista os pré-requisitos de saudação que você precisa toocomplete antes de iniciar este tutorial:

|  |Requisito |Descrição |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Dois servidores SQL | -Em um conjunto de disponibilidade do Azure <br/> -Em um único domínio <br/> -Com o recurso Cluster de Failover instalado |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Compartilhamento de arquivos para a testemunha do cluster |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta de serviço do SQL Server | Conta do domínio |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta do serviço SQL Server Agent | Conta do domínio |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Portas de firewall abertas | - SQL Server: **1433** para instância padrão <br/> - Ponto de extremidade de espelhamento de banco de dados: **5022** ou outra porta disponível <br/> - Investigação do Azure Load Balancer: **59999** ou outra porta disponível |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Adicionar o recurso Cluster de Failover à VM | Os dois SQL Servers precisam desse recurso |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Conta do domínio de instalação | - Administrador local em cada SQL Server <br/> - Membro da função de servidor fixa sysadmin do SQL Server para cada instância do SQL Server  |


Antes de começar o tutorial Olá, é necessário muito[concluir os pré-requisitos para a criação de grupos de disponibilidade AlwaysOn em máquinas virtuais Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md). Se esses pré-requisitos forem concluídos já, você pode ir muito[criar Cluster](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Criar cluster Olá

Após Olá pré-requisitos forem concluídos, Olá primeira etapa é toocreate um Cluster de Failover do Windows Server que inclui dois SQL Servers e um servidor testemunha.  

1. RDP toohello primeiro do SQL Server usando uma conta de domínio que seja um administrador nos servidores SQL e o servidor de testemunha hello.

   >[!TIP]
   >Se você seguiu Olá [documento de pré-requisitos](virtual-machines-windows-portal-sql-availability-group-prereq.md), você criou uma conta chamada **CORP\Install**. Use essa conta.

2. Em Olá **Gerenciador do servidor** painel, selecione **ferramentas**e, em seguida, clique em **Gerenciador de Cluster de Failover**.
3. No painel esquerdo do hello, clique com botão direito **Gerenciador de Cluster de Failover**e, em seguida, clique em **criar um Cluster**.
   ![Criar cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. No hello Assistente para criação de Cluster, crie um cluster de um nó percorrendo as páginas de saudação com configurações Olá Olá a tabela a seguir:

   | Página | Configurações |
   | --- | --- |
   | Antes de começar |Usar padrões |
   | Selecionar Servidores |Saudação de tipo SQL Server primeiro nome no **digite o nome do servidor** e clique em **adicionar**. |
   | Aviso de Validação |Selecione **n º eu não precisar do suporte da Microsoft para este cluster e, portanto, não quiser que a validação de saudação toorun testes. Quando clico em Avançar, continuo a criar o cluster Olá**. |
   | Ponto de acesso para administrar Olá Cluster |Digite um nome de cluster, por exemplo, **SQLAGCluster1** em **Nome do Cluster**.|
   | Confirmação |Use os padrões, a menos que você esteja usando Espaços de Armazenamento. Consulte Olá Observação Após esta tabela. |

### <a name="set-hello-cluster-ip-address"></a>Definir o endereço IP do cluster Olá

1. Em **Gerenciador de Cluster de Failover**, role para baixo demais**recursos principais de Cluster** e expanda detalhes do cluster hello. Você deverá ver dois Olá **nome** e hello **endereço IP** recursos Olá **falha** estado. Hello recurso de endereço IP não pode ser colocado online porque o cluster Olá recebeu Olá mesmo endereço IP como máquina Olá em si, portanto, ele é um endereço duplicado.

2. Com o botão direito Olá falhado **endereço IP** recursos e depois clique em **propriedades**.

   ![Propriedades do Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Selecione **endereço IP estático** e especifique um endereço disponível na sub-rede onde saudação do SQL Server está na caixa de texto endereço hello. Em seguida, clique em **OK**.
4. Em Olá **recursos principais de Cluster** seção, clique o nome do cluster e clique em **colocar Online**. Em seguida, aguarde até que ambos os recursos estejam online. Quando o recurso de nome de cluster Olá fica online, ele atualiza o servidor de DC Olá com uma nova conta de computador do AD. Use esta saudação de toorun AD conta Serviço de cluster do grupo de disponibilidade mais tarde.

### <a name="addNode"></a>Adicionar Olá outros toocluster do SQL Server

Adicionar Olá outro cluster de toohello do SQL Server.

1. Na árvore do navegador hello, mouse cluster hello e clique em **adicionar nó**.

    ![Adicionar nó toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. Em Olá **Assistente para adicionar nó**, clique em **próximo**. Em Olá **selecionar servidores** página, adicione Olá segundo servidor do SQL. Nome do servidor de saudação tipo na **digite o nome do servidor** e, em seguida, clique em **adicionar**. Quando terminar, clique em **Avançar**.

1. Em Olá **aviso de validação** , clique em **não** (em um cenário de produção, você deve executar testes de validação de saudação). Em seguida, clique em **Avançar**.

8. Em Olá **confirmação** página se você estiver usando espaços de armazenamento, Olá desmarque a caixa de seleção **adicionar todos os cluster toohello de armazenamento qualificado.**

   ![Adicionar Confirmação do Nó](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Se você estiver usando espaços de armazenamento e não desmarque **adicionar todos os armazenamento qualificado ao cluster toohello**, Windows desanexa discos virtuais Olá durante a saudação processo de clustering. Como resultado, eles não aparecem no Gerenciador de discos até que os espaços de armazenamento Olá são removidos do cluster hello e reanexados usando o PowerShell. Espaços de armazenamento agrupam vários discos em pools de toostorage. Para obter mais informações, consulte [Espaços de Armazenamento](https://technet.microsoft.com/library/hh831739).

1. Clique em **Avançar**.

1. Clique em **Concluir**.

   Gerenciador de Cluster de failover mostra que o cluster tem um novo nó e a lista em Olá **nós** contêiner.

10. Faça logoff da sessão de área de trabalho remota hello.

### <a name="add-a-cluster-quorum-file-share"></a>Adicionar um compartilhamento de arquivos de quorum de cluster

Neste exemplo o cluster do Windows hello usa um compartilhamento de arquivo toocreate um quorum de cluster. Este tutorial usa um quorum Maioria de Compartilhamento de Arquivos e Nós. Para saber mais, confira [Noções básicas sobre configurações de quorum em um cluster de failover](http://technet.microsoft.com/library/cc731739.aspx).

1. Conecte o servidor de membro de testemunha de compartilhamento de arquivo toohello com uma sessão de área de trabalho remota.

1. No **Gerenciador do Servidor**, clique em **Ferramentas**. Abra **Gerenciamento do Computador**.

1. Clique em **Pastas Compartilhadas**.

1. Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Use **criar um Assistente de pasta compartilhada** toocreate um compartilhamento.

1. Em **caminho da pasta**, clique em **procurar** e localizar ou criar um caminho de pasta compartilhada hello. Clique em **Avançar**.

1. Em **nome, descrição e configurações** Verifique se o nome de compartilhamento de saudação e o caminho. Clique em **Avançar**.

1. Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**. Clique em **Personalizar...**.

1. Em **Personalizar Permissões**, clique em **Adicionar...** .

1. Verifique se o cluster Olá Olá conta usada toocreate tem controle total.

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Clique em **OK**.

1. Em **Permissões de Pasta Compartilhada**, clique em **Concluir**. Clique em **Concluir** novamente.  

1. Faça logoff do servidor de saudação

### <a name="configure-cluster-quorum"></a>Configurar quorum do cluster

Em seguida, configure o quorum do cluster hello.

1. Conecte-se toohello primeiro nó de cluster com área de trabalho remota.

1. Em **Gerenciador de Cluster de Failover**, clique com botão direito cluster hello, aponte muito**mais ações**e clique em **Configurar Quorum do Cluster...** .

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. No **Assistente para Configurar Quorum do Cluster**, clique em **Avançar**.

1. Em **Selecionar opção de configuração de Quorum**, escolha **selecionar testemunha de quorum Olá**e clique em **próximo**.

1. Em **Selecionar Testemunha de Quorum**, clique em **Configurar testemunha de compartilhamento de arquivos**.

   >[!TIP]
   >O Windows Server 2016 dá suporte a testemunha de nuvem. Se você escolher esse tipo de testemunha, não precisará de testemunha de compartilhamento de arquivos. Para saber mais, confira [Implantar uma testemunha de nuvem para um Cluster de Failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Este tutorial usa uma testemunha de compartilhamento de arquivos, o que tem suporte de sistemas operacionais anteriores.

1. Em **configurar testemunha de compartilhamento de arquivo**, digitar o caminho de saudação para compartilhamento Olá criado. Clique em **Avançar**.

1. Verifique se as configurações de saudação em **confirmação**. Clique em **Avançar**.

1. Clique em **Concluir**.

recursos de núcleo de cluster Olá são configurados com uma testemunha de compartilhamento de arquivos.

## <a name="enable-availability-groups"></a>Habilitar Grupos de Disponibilidade

Em seguida, habilite Olá **grupos de disponibilidade do AlwaysOn** recurso. Siga estas etapas em ambos os servidores SQL.

1. De saudação **iniciar** tela, inicie **SQL Server Configuration Manager**.
2. Na árvore do navegador de saudação, clique em **serviços SQL Server**, em seguida, clique com botão direito Olá **SQL Server (MSSQLSERVER)** de serviço e clique em **propriedades**.
3. Clique em Olá **alta disponibilidade AlwaysOn** guia e, em seguida, selecione **habilitar grupos de disponibilidade do AlwaysOn**, da seguinte maneira:

    ![Habilitar Grupos de Disponibilidade AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Clique em **Aplicar**. Clique em **Okey** na caixa de diálogo pop-up hello.

5. Reinicie o serviço do SQL Server hello.

Repita essas etapas em Olá outros SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Criar um banco de dados em Olá primeiro o SQL Server

1. Iniciar Olá RDP arquivo toohello primeiro o SQL Server com um domínio de conta que é um membro da função sysadmin função de servidor fixa.
1. Abra o SQL Server Management Studio e conecte-se toohello primeiro o SQL Server.
7. No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Bancos de Dados** e em **Novo Banco de Dados**.
8. Em **Nome do banco de dados**, digite **MyDB1** e clique em **OK**.

### <a name="backupshare"></a>Criar um compartilhamento de backup

1. Em Olá primeiro o SQL Server em **Gerenciador do servidor**, clique em **ferramentas**. Abra **Gerenciamento do Computador**.

1. Clique em **Pastas Compartilhadas**.

1. Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Use **criar um Assistente de pasta compartilhada** toocreate um compartilhamento.

1. Em **caminho da pasta**, clique em **procurar** e localizar ou criar um caminho de pasta compartilhada backup do banco de dados do hello. Clique em **Avançar**.

1. Em **nome, descrição e configurações** Verifique se o nome de compartilhamento de saudação e o caminho. Clique em **Avançar**.

1. Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**. Clique em **Personalizar...**.

1. Em **Personalizar Permissões**, clique em **Adicionar...** .

1. Certifique-se de que as contas de serviço do SQL Server e o SQL Server Agent de saudação para ambos os servidores têm controle total.

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Clique em **OK**.

1. Em **Permissões de Pasta Compartilhada**, clique em **Concluir**. Clique em **Concluir** novamente.  

### <a name="take-a-full-backup-of-hello-database"></a>Faça um backup de banco de dados de saudação completo

É necessário tooback backup Olá novo banco de dados tooinitialize Olá cadeia de logs. Se você não faça um backup de banco de dados novo hello, ele não pode ser incluído em um grupo de disponibilidade.

1. Em **Pesquisador de objetos**, clique o banco de dados hello, aponte muito**tarefas...** , clique em **backup**.

1. Clique em **Okey** tootake um local de backup padrão toohello backup completo.

## <a name="create-hello-availability-group"></a>Criar hello grupo de disponibilidade
Agora você está pronto tooconfigure um grupo de disponibilidade usando Olá seguindo as etapas:

* Criar um banco de dados em Olá primeiro o SQL Server.
* Faça um backup completo e um backup de log de transações do banco de dados de saudação
* Saudação de restauração completa e toohello de backups de log segundo do SQL Server com hello **NORECOVERY** opção
* Criar hello grupo de disponibilidade (**AG1**) com confirmação síncrona, failover automático e réplicas secundárias legíveis

### <a name="create-hello-availability-group"></a>Crie hello grupo de disponibilidade:

1. Na sessão de área de trabalho remota toohello primeiro o SQL Server. Em **Pesquisador de Objetos** no SSMS, clique com o botão direito do mouse em **Alta Disponibilidade AlwaysOn** e clique em **Assistente de Novo Grupo de Disponibilidade**.

    ![Inicie o Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. Em Olá **Introdução** , clique em **próximo**. Em Olá **especificar nome do grupo de disponibilidade** página, digite um nome para Olá grupo de disponibilidade, por exemplo **AG1**, na **nome do grupo de disponibilidade**. Clique em **Avançar**.

    ![Novo assistente de AG, especifique o nome do AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. Em Olá **Selecionar bancos de dados** , selecione o banco de dados e clique em **próximo**.

   >[!NOTE]
   >banco de dados de saudação atende aos pré-requisitos de saudação para um grupo de disponibilidade porque você ter obtido pelo menos um backup completo na réplica primária pretendida de saudação.

   ![Novo assistente AG, selecione os bancos de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. Em Olá **especificar réplicas** , clique em **adicionar réplica**.

   ![Novo assistente AG, especifique as réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Olá **conectar tooServer** caixa de diálogo será exibida. Nome de saudação do tipo do segundo servidor de saudação em **nome do servidor**. Clique em **Conectar**.

   Em Olá **especificar réplicas** página, você verá agora listado no segundo servidor de saudação **réplicas de disponibilidade**. Configure réplicas de saudação da seguinte maneira.

   ![Novo assistente de AG, Especificar Réplicas (Completo)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Clique em **pontos de extremidade** banco de dados do hello toosee ponto de extremidade de espelhamento para este grupo de disponibilidade. Olá Use mesma porta que você usou ao configurar Olá [regra de firewall para pontos de extremidade de espelhamento de banco de dados](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. Em Olá **selecionar sincronização de dados inicial** , selecione **completo** e especifique um local de rede compartilhada. Para o local do hello, use Olá [compartilhamento de backup que você criou](#backupshare). No exemplo hello era, **\\\\\<primeiro servidor do SQL\>\Backup\**. Clique em **Avançar**.

   >[!NOTE]
   >Sincronização completa usa um backup completo do banco de dados de saudação na primeira instância de saudação do SQL Server e restaurá-lo toohello segunda instância. Em caso de grandes bancos de dados, a sincronização completa não é recomendada porque pode levar muito tempo. Você pode reduzir esse tempo manualmente fazer um backup de banco de dados de saudação e restaurando-o com `NO RECOVERY`. Se o banco de dados de saudação já é restaurado com `NO RECOVERY` em Olá segundo do SQL Server antes de configurar Olá grupo de disponibilidade, escolha **somente junção**. Backup de saudação tootake depois de configurar Olá grupo de disponibilidade, escolha **ignorar sincronização de dados inicial**.

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. Em Olá **validação** , clique em **próximo**. Esta página deve ser semelhante toohello imagem a seguir:

    ![Novo assistente AG, Validação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Há um aviso para configuração de ouvinte Olá porque você não configurou um ouvinte de grupo de disponibilidade. Você pode ignorar este aviso porque em máquinas virtuais do Azure criar ouvinte Olá depois de criar o balanceador de carga do Azure hello.

10. Em Olá **resumo** , clique em **concluir**, em seguida, aguarde enquanto o Assistente de saudação configura Olá novo grupo de disponibilidade. Em Olá **andamento** página, você pode clicar em **mais detalhes** tooview Olá detalhadas progresso. Quando a saudação assistente for concluído, inspecione Olá **resultados** tooverify de página que Olá grupo de disponibilidade é criado com êxito.

     ![Novo assistente de AG, Resultados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Clique em **fechar** tooexit Assistente de saudação.

### <a name="check-hello-availability-group"></a>Saudação de verificação de grupo de disponibilidade

1. Em **Pesquisador de Objetos**, expanda **Alta Disponibilidade AlwaysOn** e expanda **Grupos de Disponibilidade**. Agora você deve ver Olá novo grupo de disponibilidade neste contêiner. Olá grupo de disponibilidade de mouse e clique em **Mostrar painel**.

   ![Mostrar Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   O **painel AlwaysOn** deve ter aparência semelhante toothis.

   ![Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Você pode ver réplicas hello, modo de failover Olá cada réplica e saudação do estado de sincronização.

2. No **Gerenciador de Cluster de Failover**, clique em seu cluster. Selecione **funções**. nome do grupo de disponibilidade Olá usado é uma função em cluster hello. Esse Grupo de Disponibilidade não tem um endereço IP para conexões de cliente porque você não configurou um ouvinte. Você irá configurar o ouvinte Olá depois de criar um balanceador de carga do Azure.

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Não tente toofail sobre Olá grupo de disponibilidade do hello Gerenciador de Cluster de Failover. Todas as operações de failover devem ser executadas no **Painel AlwaysOn** no SSMS. Para obter mais informações, consulte [restrições usando Olá Gerenciador de Cluster de Failover com grupos de disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).
    >

Agora você tem um Grupo de Disponibilidade com réplicas em duas instâncias do SQL Server. Você pode mover Olá grupo de disponibilidade entre instâncias. Você não pode se conectar toohello grupo de disponibilidade ainda não tiver um ouvinte. Em máquinas virtuais do Azure, o ouvinte de saudação exige um balanceador de carga. Olá próxima etapa é toocreate balanceador de carga Olá no Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Criar um balanceador de carga do Azure

Nas máquinas virtuais do Azure, um Grupo de Disponibilidade do SQL Server precisa de um balanceador de carga. Balanceador de carga Olá contém o endereço IP de Olá para o ouvinte de grupo de disponibilidade de saudação. Esta seção resume como toocreate Olá balanceador de carga no hello portal do Azure.

1. No hello portal do Azure, vá toohello grupo de recursos onde os SQL Servers estão e clique em **+ adicionar**.
2. Pesquise pelo **Balanceador de Carga**. Escolha o balanceador de carga Olá publicado pela Microsoft.

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Clique em **Criar**.
3. Configure Olá parâmetros Olá balanceador de carga a seguir.

   | Configuração | Campo |
   | --- | --- |
   | **Nome** |Use um nome para o balanceador de carga hello, por exemplo **sqlLB**. |
   | **Tipo** |Interna |
   | **Rede virtual** |Use nome de saudação do hello rede virtual do Azure. |
   | **Sub-rede** |Use o nome de saudação da sub-rede Olá Olá a máquina virtual está em.  |
   | **Atribuição de endereço IP** |Estático |
   | **Endereço IP** |Use um endereço disponível da sub-rede. |
   | **Assinatura** |Use Olá a mesma assinatura que a máquina virtual de saudação. |
   | **Localidade** |Use Olá mesmo local que a máquina virtual de saudação. |

   Olá folha portal do Azure deve ter esta aparência:

   ![Criar balanceador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Clique em **criar**, balanceador de carga toocreate hello.

Balanceador de carga de saudação tooconfigure, é necessário toocreate um pool de back-end, uma investigação e regras de balanceamento de carga de Olá conjunto. Siga estes procedimentos na Olá portal do Azure.

### <a name="add-backend-pool"></a>Adicionar pool de back-end

1. No hello portal do Azure, vá tooyour o grupo de disponibilidade. Talvez seja necessário balanceador de carga toorefresh Olá exibição toosee Olá recém-criado.

   ![Encontrar o Balanceador de Carga no Grupo de Recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Clique em balanceador de carga Olá, **pools de back-end**e clique em **+ adicionar**. Configure o pool de back-end de saudação da seguinte maneira:

   | Configuração | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Digite um nome de texto | SQLLBBE
   | **Associado a** | Selecione uma opção na lista | Conjunto de disponibilidade
   | **Conjunto de disponibilidade** | Use um nome de conjunto de disponibilidade de saudação que suas VMs do SQL Server estão em | sqlAvailabilitySet |
   | **Máquinas virtuais** |Olá dois nomes de VM do Azure SQL Server | sqlserver-0, sqlserver-1

1. Digite o nome de saudação para pool de back-end de saudação.

1. Clique em **+ Adicionar uma máquina virtual**.

1. Para conjunto de disponibilidade hello, escolha conjunto de disponibilidade de saudação que Olá SQL Servers estão no.

1. Para máquinas virtuais, incluem ambos Olá SQL Servers. Não inclua o servidor de testemunha de compartilhamento de arquivo hello.

1. Clique em **Okey** toocreate pool de back-end de saudação.

### <a name="set-hello-probe"></a>Investigação de saudação do conjunto

1. Clique em balanceador de carga Olá, **sondas de integridade**e clique em **+ adicionar**.

1. Defina investigação de integridade de saudação da seguinte maneira:

   | Configuração | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Texto | SQLAlwaysOnEndPointProbe |
   | **Protocolo** | Escolher TCP | TCP |
   | **Porta** | Qualquer porta não utilizada | 59999 |
   | **Intervalo**  | quantidade de saudação de tempo entre a investigação tentativas em segundos |5 |
   | **Limite não íntegro** | Olá número de falhas de investigação consecutivas que deve ocorrer para um toobe de máquina virtual considerado não íntegro  | 2 |

1. Clique em **Okey** tooset investigação de integridade de saudação.

### <a name="set-hello-load-balancing-rules"></a>Definir regras de balanceamento de carga de Olá

1. Clique em balanceador de carga Olá, **regras de balanceamento de carga**e clique em **+ adicionar**.

1. Defina a saudação de balanceamento de carga regras da seguinte maneira.
   | Configuração | Descrição | Exemplo
   | --- | --- |---
   | **Nome** | Texto | SQLAlwaysOnEndPointListener |
   | **Endereço IP de front-end** | Escolher um endereço |Use endereço Olá criada quando criou o balanceador de carga de saudação. |
   | **Protocolo** | Escolher TCP |TCP |
   | **Porta** | Usar porta Olá Olá instância do SQL Server | 1433 |
   | **Porta de back-end** | Este campo não é usado quando o IP flutuante é definido para o retorno de servidor direto | 1433 |
   | **Investigação** |nome de saudação especificado para investigação Olá | SQLAlwaysOnEndPointProbe |
   | **Persistência de sessão** | Lista suspensa | **Nenhum** |
   | **Tempo limite de ociosidade** | Minutos tookeep abrir uma conexão TCP | 4 |
   | **IP flutuante (retorno de servidor direto)** | |Habilitado |

   > [!WARNING]
   > O retorno de servidor direto é definido durante a criação. Ele não pode ser alterado.

1. Clique em **Okey** regras de balanceamento de carga de saudação de tooset.

## <a name="configure-listener"></a>Configurar ouvinte Olá

Olá próxima coisa toodo é tooconfigure um ouvinte de grupo de disponibilidade no cluster de failover de saudação.

> [!NOTE]
> Este tutorial mostra como tratar toocreate um ouvinte único - com um IP do ILB. toocreate um ou mais ouvintes usando um ou mais endereços IP, consulte [balanceador de carga e de ouvinte criar grupo de disponibilidade | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Definir porta do ouvinte

No SQL Server Management Studio, defina a porta do ouvinte hello.

1. Inicie o SQL Server Management Studio e conecte-se a réplica primária toohello.

1. Navegue muito**alta disponibilidade AlwaysOn** | **grupos de disponibilidade** | **ouvintes do grupo de disponibilidade**.

1. Agora você deve ver o nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover. Nome do ouvinte de saudação de mouse e clique em **propriedades**.

1. Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade de saudação usando Olá $EndpointPort utilizado antes (1433 foi padrão Olá), em seguida, clique em **Okey**.

Agora você tem um Grupo de Disponibilidade do SQL Server em máquinas virtuais do Azure, em execução no modo de Resource Manager.

## <a name="test-connection-toolistener"></a>Toolistener de conexão de teste

conexão de saudação tootest:

1. RDP tooa SQL Server que está em Olá mesmo virtual de rede, mas não não réplica Olá próprio. Você pode usar Olá outros SQL Server em cluster hello.

1. Use **sqlcmd** conexão de saudação do utilitário tootest. Por exemplo, a saudação script a seguir estabelece uma **sqlcmd** réplica primária de toohello de conexão por meio do ouvinte Olá com autenticação do Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Se o ouvinte Olá estiver usando uma porta diferente de Olá padrão (1433) de porta, especifique a porta Olá na cadeia de caracteres de conexão de saudação. Por exemplo, hello seguinte comando sqlcmd conecta tooa escuta na porta 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Olá conexão SQLCMD conecta-se automaticamente toowhichever instância do SQL Server hospeda Olá a réplica primária.

> [!TIP]
> Certifique-se de que a porta de Olá especificado é aberta no firewall Olá de ambos os servidores SQL. Ambos os servidores exigem uma regra de entrada para Olá a porta TCP que você usa. Para saber mais, confira [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Próximas etapas

- [Adicionar um balanceador de carga tooa de endereço IP para um segundo grupo de disponibilidade](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
