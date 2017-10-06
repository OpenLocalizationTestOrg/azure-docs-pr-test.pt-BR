---
title: "aaaDistributed transações entre bancos de dados de nuvem"
description: "Visão Geral das Transações de Banco de Dados Elástico com o Banco de Dados SQL do Azure"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Transações distribuídas entre bancos de dados na nuvem
Transações de banco de dados Elástico de banco de dados do SQL do Azure (banco de dados SQL) permitem que você toorun transações que abrangem vários bancos de dados no banco de dados SQL. Transações de banco de dados Elástico de banco de dados SQL estão disponíveis para aplicativos .NET usando o ADO .NET e integrar com experiência programação familiar hello usando Olá [Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) classes. biblioteca de saudação tooget, consulte [do .NET Framework 4.6.1 (instalador da Web)](https://www.microsoft.com/download/details.aspx?id=49981).

No local, esse cenário normalmente exigiria a execução do recurso MSDTC (Coordenador de Transações Distribuídas da Microsoft). Desde que o MSDTC não está disponível para aplicativos de plataforma como um serviço no Azure, transações de toocoordinate distribuída capacidade Olá agora foi diretamente integrado ao banco de dados SQL. Aplicativos podem se conectar a tooany transações de toolaunch distribuído de banco de dados SQL e um dos bancos de dados de saudação transparentemente coordena transações Olá distribuída, conforme mostrado na figura a seguir de saudação. 

  ![Transações distribuídas com o Banco de Dados SQL do Azure usando transações de banco de dados elástico ][1]

## <a name="common-scenarios"></a>Cenários comuns
Transações de banco de dados Elástico de banco de dados SQL habilitar aplicativos toomake mudanças atômicas toodata armazenado em vários bancos de dados diferentes do SQL. visualização de saudação se concentra em experiências de desenvolvimento de cliente em c# e .NET. Há planos para uma experiência do lado do servidor usando o T-SQL para um momento posterior.  
Saudação de destinos de transações de banco de dados Elástico os seguintes cenários:

* Aplicativos de vários bancos de dados no Azure: com esse cenário, os dados são particionados verticalmente em vários bancos de dados no BD SQL, de modo que os diferentes tipos de dados residam em bancos de dados diferentes. Algumas operações exigem toodata alterações que é mantido em duas ou mais bancos de dados. aplicativo Hello usa as alterações do banco de dados Elástico transações toocoordinate Olá em bancos de dados e garantir a atomicidade.
* Aplicativos de banco de dados fragmentado no Azure: com esse cenário, a camada de dados de Olá usa Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md) ou autofragmentação toohorizontally partição Olá dados em vários bancos de dados no banco de dados SQL. Um caso de uso proeminentes é mudanças atômicas do hello necessidade tooperform para um aplicativo multilocatário fragmentado quando alterações abrangem locatários. Considere para a instância de uma transferência de um locatário tooanother, ambos os que residem em bancos de dados diferentes. Um segundo caso é fragmentação refinada tooaccommodate necessidades de capacidade para um locatário grande, que por sua vez, normalmente, implica que algumas toostretch de necessidades de operações atômicas em vários bancos de dados usados para Olá mesmo locatário. Um terceiro caso é atômica atualiza os dados de tooreference que são replicados em bancos de dados. Operações atômicas transacionadas, essas linhas agora podem ser coordenadas entre vários bancos de dados usando a visualização de saudação.
  Transações de banco de dados Elástico usam atomicidade do protocolo 2PC tooensure transações entre bancos de dados. É uma boa opção para as transações que envolvem menos de 100 bancos de dados por vez em uma única transação. Esses limites não são impostos, mas um deve esperar o desempenho e taxas de sucesso para o banco de dados Elástico transações toosuffer ao exceder esses limites.

## <a name="installation-and-migration"></a>Instalação e migração
recursos de saudação para transações de banco de dados Elástico no banco de dados SQL são fornecidos por meio de bibliotecas do .NET toohello de atualizações System.Data.dll e System.Transactions.dll. Olá DLLs Certifique-se de confirmação de duas fases é usada quando necessário tooensure atomicidade. instalar toostart desenvolver aplicativos usando transações de banco de dados Elástico [do .NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) ou uma versão posterior. Quando executado em uma versão anterior do .NET framework do hello, haverá falha nas transações toopromote tooa distribuída transaction e será gerada uma exceção.

Após a instalação, você pode usar transações distribuída de saudação APIs System. Transactions com conexões tooSQL banco de dados. Se você tiver aplicativos existentes do MSDTC usando essas APIs, simplesmente recriar seus aplicativos existentes para o .NET 4.6 depois de instalar o hello 4.6.1 Framework. Se seus projetos de destino do .NET 4.6, eles usarão automaticamente DLLs Olá atualizado da versão do Framework novo hello e chamadas de API de transação distribuída em combinação com conexões tooSQL que DB agora terá êxito.

Lembre-se de que as transações de banco de dados elástico não requerem a instalação do MSDTC. Em vez disso, as transações de banco de dados elástico são gerenciadas diretamente pelo BD SQL, dentro dele. Isso simplifica significativamente a cenários de nuvem como uma implantação do MSDTC não é necessário toouse distribuída transações com o banco de dados SQL. Seção 4 explica detalhadamente como hello e transações de banco de dados Elástico toodeploy necessária do .NET framework junto com seu tooAzure de aplicativos de nuvem.

## <a name="development-experience"></a>Experiência de desenvolvimento
### <a name="multi-database-applications"></a>Aplicativos de vários bancos de dados
Olá código a seguir usa experiência familiar de programação Olá com .NET System. Transactions. Olá classe TransactionScope estabelece uma transação de ambiente no .NET. (Uma "transação de ambiente" é um que reside no thread atual hello.) Todas as conexões abertas em Olá TransactionScope participarem de transações de saudação. Se participarem de bancos de dados diferentes, a transação de Olá é automaticamente elevada tooa distribuída transação. resultado de saudação da transação de saudação é controlado pela configuração Olá escopo toocomplete tooindicate uma confirmação.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Aplicativos de banco de dados fragmentado
Transações de banco de dados Elástico de banco de dados SQL também dão suporte a coordenação de transações distribuídas, onde você utiliza o método de OpenConnectionForKey Olá Olá Elástico de banco de dados biblioteca tooopen de conexões de cliente para uma expansão de dados camada. Considere a possibilidade de casos onde você precisa consistência transacional tooguarantee para alterações em vários valores de chave de fragmentação diferente. Fragmentos de toohello conexões hospedagem valores de chave de fragmentação diferente de saudação são orientados usando OpenConnectionForKey. No caso de geral hello, conexões Olá podem ser toodifferent fragmentos, de modo que garantir garantias transacionais requer uma transação distribuída. saudação de exemplo de código a seguir ilustra essa abordagem. Ele pressupõe que uma variável chamada shardmap é toorepresent usado um fragmento do mapa da biblioteca de cliente do banco de dados Elástico hello:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Instalação do .NET para os Serviços de Nuvem do Azure
O Azure fornece várias ofertas de aplicativos .NET de toohost. Uma comparação entre as diferentes ofertas hello está disponível em [comparação do serviço de aplicativo do Azure, serviços de nuvem e máquinas virtuais](../app-service-web/choose-web-site-cloud-service-vm.md). Se hello a sistema operacional convidado da oferta de saudação é menor do que o .NET 4.6.1 exigido para transações Elásticos, será necessário tooupgrade too4.6.1 de sistema operacional de convidado de saudação. 

Para serviços de aplicativo do Azure, atualiza convidado toohello que SO não têm suporte no momento. Para máquinas de virtuais do Azure, basta fazer logon em Olá VM e executar o instalador de saudação do hello mais recente do .NET framework. Para serviços de nuvem do Azure, você precisa de instalação de saudação tooinclude de uma versão mais recente do .NET em tarefas de inicialização de saudação da sua implantação. conceitos de saudação e as etapas documentadas no [instalar .NET em uma função de serviço de nuvem](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Observe que Olá instalador para o .NET 4.6.1 pode exigir mais armazenamento temporário durante a saudação inicializar processo nos serviços de nuvem do Azure que Olá instalador para o .NET 4.6. tooensure uma instalação bem-sucedida, é necessário armazenamento temporário tooincrease para seu serviço de nuvem do Azure em seu arquivo servicedefinition. Csdef na seção de LocalResources Olá Olá configurações do ambiente e de sua tarefa de inicialização, conforme mostrado na seguinte Olá exemplo:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transações entre vários servidores
Há suporte para transações de Banco de Dados Elástico entre diferentes servidores lógicos no Banco de Dados SQL do Azure. Quando as transações cruzam os limites do servidor lógico, servidores participantes Olá primeiro necessário toobe inserido em uma relação de comunicação comum. Após o estabelecimento de relação de comunicação hello, qualquer banco de dados em qualquer um dos Olá dois servidores podem participar de transações Elásticos com bancos de dados de Olá outro servidor. Com mais de dois servidores lógicos a abrangência de transações, uma relação de comunicação deve toobe em vigor para qualquer par de servidores lógicos.

Use Olá relações de comunicação entre servidores de toomanage PowerShell cmdlets para transações de banco de dados Elástico a seguir:

* **Novo AzureRmSqlServerCommunicationLink**: Use esse cmdlet toocreate uma nova relação de comunicação entre dois servidores lógicos no banco de dados de SQL do Azure. relação de saudação for simétrica, que significa que ambos os servidores podem iniciar transações com hello outro servidor.
* **Get-AzureRmSqlServerCommunicationLink**: Use essa comunicação existente do cmdlet tooretrieve relações e suas propriedades.
* **Remover AzureRmSqlServerCommunicationLink**: Use esse cmdlet tooremove uma relação de comunicação existente. 

## <a name="monitoring-transaction-status"></a>Monitorando o status da transação
Use as exibições de gerenciamento dinâmico (DMVs) no banco de dados SQL toomonitor status e progresso das suas transações de banco de dados Elástico em andamento. Todos os tootransactions relacionados de DMVs são relevantes para transações distribuídas no banco de dados SQL. Você pode encontrar hello lista correspondente DMVs aqui: [relacionados exibições de gerenciamento dinâmico transação e funções (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Estas DMVs são especialmente úteis:

* **sys.dm\_tran\_active\_transactions**: lista as transações atualmente ativas e seu status. Olá coluna UOW (unidade de trabalho) pode identificar Olá filho diferentes transações que pertencem a toohello mesma transação distribuída. Todas as transações dentro Olá mesma transação distribuída realizar Olá mesmo valor UOW. Consulte Olá [documentação DMV](https://msdn.microsoft.com/library/ms174302.aspx) para obter mais detalhes.
* **sys.DM\_tran\_banco de dados\_transações**: fornece informações adicionais sobre transações, como o posicionamento de transação Olá no log de saudação. Consulte Olá [documentação DMV](https://msdn.microsoft.com/library/ms186957.aspx) para obter mais detalhes.
* **sys.DM\_tran\_bloqueios**: fornece informações sobre bloqueios de saudação que são mantidos por transações em andamento. Consulte Olá [documentação DMV](https://msdn.microsoft.com/library/ms190345.aspx) para obter mais detalhes.

## <a name="limitations"></a>Limitações
Olá seguintes limitações no momento se aplicam a tooelastic transações de banco de dados no banco de dados SQL:

* Há suporte somente para transações em bancos de dados no BD SQL. Outros provedores de recursos [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) e bancos de dados fora do BD SQL não podem participar de transações de banco de dados elástico. Isso significa que as transações de banco de dados elástico não podem se estender para o SQL Server e o Banco de Dados SQL do Azure no local. Para transações distribuídas no local, continue toouse MSDTC. 
* Há suporte somente para transações coordenadas pelo cliente a partir de um aplicativo .NET. Há planos para suporte do lado do servidor para o T-SQL, como INICIAR TRANSAÇÃO DISTRIBUÍDA, mas ainda não está disponível. 
* Não há suporte para transações em serviços WCF. Por exemplo, você tem um método de serviço WCF que executa uma transação. Olá chamada dentro de um escopo de transação de circunscrição falhará como um [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Próximas etapas
Para dúvidas, entre em contato toous em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e para solicitações de recurso, adicione-toohello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



