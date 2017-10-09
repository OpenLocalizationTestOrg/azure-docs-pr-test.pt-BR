---
title: regras de firewall de banco de dados SQL aaaAzure | Microsoft Docs
description: "Saiba como tooconfigure um SQL de banco de dados firewall com acesso de toomanage de regras de firewall no nível de servidor e nível de banco de dados."
keywords: firewall do banco de dados
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Regras de firewall de nível do servidor de banco de dados do Banco de Dados SQL do Azure 

O Banco de Dados SQL do Microsoft Azure fornece um serviço de banco de dados relacional para o Azure e outros aplicativos baseados na Internet. toohelp proteger seus dados, firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede acesso toodatabases com base em Olá endereços IP de cada solicitação de origem.

## <a name="overview"></a>Visão geral

Inicialmente, todos os do Azure SQL server Transact-SQL acesso tooyour é bloqueado pelo firewall de saudação. toobegin usando seu servidor do SQL Azure, você deve especificar uma ou mais regras de firewall de nível de servidor que permitem acesso tooyour Azure do SQL server. Use toospecify de regras de firewall Olá qual endereço IP varia de saudação Internet são permitidos, e se os aplicativos do Azure podem tentar tooconnect tooyour SQL do Azure server.

tooselectively conceder acesso toojust um Olá bancos de dados em seu servidor do SQL Azure, você deve criar uma regra de nível de banco de dados do banco de dados necessário hello. Especifique um intervalo de endereços IP para regra de firewall do banco de dados Olá ultrapassa Olá especificado na regra de firewall no nível de servidor de saudação do intervalo de endereços IP e certifique-se de que o endereço IP de saudação do cliente de saudação esteja no intervalo de saudação especificado na regra de nível de banco de dados de saudação.

Olá de tentativas de Conexão de Internet e o Azure deve passar primeiramente pelo firewall Olá antes de poderem acessar seu servidor do SQL Azure ou o banco de dados SQL, conforme mostrado no diagrama a seguir de saudação:

   ![Diagrama descrevendo a configuração de firewall.][1]

* **Regras de firewall de nível de servidor:** essas regras permitem que os clientes tooaccess o servidor inteiro do SQL Azure, ou seja, todos os bancos de dados de saudação em Olá mesmo servidor lógico. Essas regras são armazenadas em Olá **mestre** banco de dados. Regras de firewall de nível de servidor podem ser configuradas usando o portal de saudação ou usando instruções Transact-SQL. regras de firewall de nível de servidor toocreate usando Olá portal do Azure ou o PowerShell, você deve ser o proprietário da assinatura hello ou um colaborador da assinatura. toocreate uma regra de firewall de nível de servidor usando o Transact-SQL, você deve conectar a instância de banco de dados SQL toohello como logon principal no nível de servidor hello ou administrador do Active Directory do Azure hello (o que significa que uma regra de firewall de nível de servidor deve ser criada primeiro por um usuário com permissões no nível do Azure).
* **Regras de firewall de nível de banco de dados:** essas regras permitem que clientes tooaccess determinados (seguro) bancos de dados dentro de saudação mesmo servidor lógico. Você pode criar essas regras para cada banco de dados (incluindo Olá **mestre** database0) e são armazenados em bancos de dados individuais hello. Regras de firewall de nível de banco de dados só podem ser configuradas usando instruções Transact-SQL e somente depois que você configurou Olá primeiro firewall no nível de servidor. Se você especificar um intervalo de endereços IP na regra de firewall no nível de banco de dados de saudação que é especificado na regra de firewall no nível de servidor de saudação do intervalo de saudação fora, somente aqueles clientes que têm endereços IP no intervalo de nível de banco de dados de saudação acessar Olá banco de dados. Você pode ter no máximo 128 regras de firewall no nível do banco de dados para um banco de dados. Somente é possível criar e gerenciar regras de firewall no nível de banco de dados para bancos de dados mestre e de usuário por meio o Transact-SQL. Para obter mais informações sobre como configurar regras de firewall de nível de banco de dados, consulte o exemplo hello adiante neste artigo e veja [sp_set_database_firewall_rule (bancos de dados do SQL Azure)](https://msdn.microsoft.com/library/dn270010.aspx).

**Recomendação:** Microsoft recomenda o uso de regras de firewall de nível de banco de dados sempre que possível tooenhance segurança e toomake seu banco de dados mais portáteis. Usar regras de firewall de nível de servidor para administradores e quando você tem muitos bancos de dados que têm Olá mesmos requisitos de acesso e você não desejar tempo toospend configurar cada banco de dados individualmente.

> [!Note]
> Para obter informações sobre bancos de dados portátil no contexto de saudação de continuidade de negócios, consulte [requisitos de autenticação para a recuperação de desastres](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>Conectando-se de saudação da Internet

Quando um computador tenta tooconnect tooyour servidor de banco de dados de saudação da Internet, firewall Olá verifica primeiro Olá endereços IP da solicitação de saudação em relação a regras de firewall no nível de banco de dados hello, do banco de dados de saudação que está solicitando a conexão de saudação de origem:

* Se Olá endereço IP de saudação solicitação estiver dentro de um dos intervalos de saudação especificados nas regras de firewall de nível de banco de dados de hello, conexão Olá será concedida toohello banco de dados SQL que contém a regra de saudação.
* Se Olá endereço IP de saudação solicitação não estiver dentro de um dos intervalos de saudação especificados na regra de firewall no nível de banco de dados hello, regras de firewall no nível de servidor de saudação são verificadas. Se Olá endereço IP de saudação solicitação estiver dentro de um dos intervalos de saudação especificados nas regras de firewall de nível de servidor de saudação, conexão Olá será concedida. Regras de firewall de nível de servidor se aplicam a tooall bancos de dados SQL no servidor do SQL Azure hello.  
* Se Olá endereço IP de saudação solicitação não está dentro de intervalos de saudação especificado em qualquer Olá nível de banco de dados ou regras de firewall no nível de servidor, falha de solicitação de conexão de saudação.

> [!NOTE]
> tooaccess banco de dados SQL do computador local, certifique-se de firewall Olá na sua rede e o computador local permita a comunicação de saída na porta TCP 1433.
> 

### <a name="connecting-from-azure"></a>Conexão pelo Azure
tooallow aplicativos do Azure tooconnect tooyour servidor SQL do Azure, as conexões do Azure devem ser habilitados. Quando um aplicativo do Azure tenta o servidor de banco de dados de tooyour tooconnect, firewall Olá verifica que são permitidas conexões do Azure. Uma configuração de firewall com inicial e final too0.0.0.0 igual endereço indica que essas conexões são permitidas. Se a tentativa de conexão de saudação não é permitida, solicitação Olá não alcançar o servidor de banco de dados do Azure SQL hello.

> [!IMPORTANT]
> Esta opção configura Olá firewall tooallow todas as conexões do Azure conexões incluindo de assinaturas de saudação de outros clientes. Quando esta opção, verifique se seu logon e permissões de usuário limitam tooonly acesso a usuários autorizados.
> 

## <a name="creating-and-managing-firewall-rules"></a>Criar e gerenciar regras de firewall
configuração de firewall no nível de servidor primeiro Olá pode ser criada usando Olá [portal do Azure](https://portal.azure.com/) ou programaticamente usando [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [CLI do Azure](/cli/azure/sql/server/firewall-rule#create), ou hello [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). As regras de firewall no nível de servidor subsequentes podem ser criadas e gerenciados usando esses métodos e por meio de Transact-SQL. 

> [!IMPORTANT]
> As regras de firewall no nível de banco de dados só podem ser criadas e gerenciadas usando com o Transact-SQL. 
>

desempenho tooimprove, regras são temporariamente armazenados em cache no nível de banco de dados de saudação de firewall de nível de servidor. cache de saudação toorefresh, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> Você pode usar [auditoria de banco de dados SQL](sql-database-auditing.md) tooaudit alterações de firewall no nível de servidor e nível de banco de dados.
>

### <a name="azure-portal"></a>Portal do Azure

tooset uma regra de firewall de nível de servidor em Olá portal do Azure, você pode ir página de visão geral do toohello ou para a sua página de visão geral de saudação ou de banco de dados SQL do Azure para seu servidor lógico do banco de dados do Azure.

> [!TIP]
> Para obter um tutorial, consulte [criar um banco de dados usando Olá portal do Azure](sql-database-get-started-portal.md).
>

**Na página de visão geral de banco de dados**

1. tooset uma regra de firewall de nível de servidor na página de visão geral do banco de dados de saudação, clique em **definir o firewall do servidor** na barra de ferramentas Olá conforme Olá a imagem a seguir: Olá **configurações de Firewall** página Olá SQL Servidor de banco de dados será aberto.

      ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Clique em **Adicionar IP do cliente** no endereço IP de Olá Olá barra de ferramentas tooadd do computador Olá você está usando no momento e, em seguida, clique em **salvar**. Uma regra de firewall no nível do servidor é criada para seu endereço IP atual.

      ![definir regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Da página de visão geral de servidor**

Olá, página de visão geral para server abre, mostrando a você Olá totalmente qualificado nome do servidor (como **mynewserver20170403.database.windows.net**) e fornece opções de configuração adicional.

1. tooset uma regra de nível de servidor na página de visão geral do servidor, clique em **Firewall** no menu esquerdo de saudação em configurações, conforme mostrado em Olá a imagem a seguir: 

     ![visão geral do servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Clique em **Adicionar IP do cliente** no endereço IP de Olá Olá barra de ferramentas tooadd do computador Olá você está usando no momento e, em seguida, clique em **salvar**. Uma regra de firewall no nível do servidor é criada para seu endereço IP atual.

     ![definir regra de firewall do servidor](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Exibição do catálogo ou Procedimento armazenado | Nível | Descrição |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Servidor |Exibe regras de firewall no nível de servidor atual Olá |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Servidor |Cria ou atualiza as regras de firewall no nível de servidor |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Servidor |Remove as regras de firewall no nível de servidor |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Banco de dados |Exibe regras de firewall no nível de banco de dados atual Olá |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Banco de dados |Cria ou atualiza regras de firewall no nível de banco de dados de saudação |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Bancos de dados |Remove as regras de firewall no nível de banco de dados |


Hello exemplos a seguir examine as regras existentes hello, habilitar um intervalo de endereços IP no servidor de saudação Contoso e exclui uma regra de firewall:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
Em seguida, adicione uma regra de firewall.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete uma regra de firewall de nível de servidor, executar o procedimento de sp_delete_firewall_rule armazenado hello. Olá exemplo a seguir exclui a regra de saudação nomeada ContosoFirewallRule:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Nível | Descrição |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Servidor |Retorna as regras atuais de firewall de nível de servidor Olá |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Servidor |Cria as regras de firewall no nível de servidor |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Servidor |Atualiza as propriedades de saudação de uma regra de firewall de nível de servidor existente |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Servidor |Remove as regras de firewall no nível de servidor |


saudação de exemplo a seguir define uma regra de firewall de nível de servidor usando o PowerShell:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> Para exemplos do PowerShell no contexto de saudação de um início rápido, consulte [criar banco de dados - PowerShell](sql-database-get-started-powershell.md) e [criar um banco de dados e configurar uma regra de firewall usando o PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>CLI do Azure
| Cmdlet | Nível | Descrição |
| --- | --- | --- |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Cria um firewall regra tooallow acesso tooall bancos de dados SQL no servidor de saudação do intervalo de endereços IP hello inserido.|
| [az sql server firewall delete](/cli/azure/sql/server/firewall-rule#delete)| Exclui uma regra de firewall.|
| [az sql server firewall list](/cli/azure/sql/server/firewall-rule#list)| Lista as regras de firewall hello.|
| [az sql server firewall rule show](/cli/azure/sql/server/firewall-rule#show)| Mostra detalhes de saudação de uma regra de firewall.|
| [ax sql server firewall rule update](/cli/azure/sql/server/firewall-rule#update)| Atualiza uma regra de firewall.

saudação de exemplo a seguir define uma regra de firewall de nível de servidor usando Olá CLI do Azure: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Para obter um exemplo de CLI do Azure no contexto de saudação de um início rápido, consulte [criar BDD - CLI do Azure](sql-database-get-started-cli.md) e [criar um banco de dados e configurar uma regra de firewall usando Olá CLI do Azure](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>API REST
| API | Nível | Descrição |
| --- | --- | --- |
| [Listar regras de firewall](https://msdn.microsoft.com/library/azure/dn505715.aspx) |Servidor |Exibe regras de firewall no nível de servidor atual Olá |
| [Criar uma regra de firewall](https://msdn.microsoft.com/library/azure/dn505712.aspx) |Servidor |Cria ou atualiza as regras de firewall no nível de servidor |
| [Definir regra de firewall](https://msdn.microsoft.com/library/azure/dn505707.aspx) |Servidor |Atualiza as propriedades de saudação de uma regra de firewall de nível de servidor existente |
| [Excluir regra de firewall](https://msdn.microsoft.com/library/azure/dn505706.aspx) |Servidor |Remove as regras de firewall no nível de servidor |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Regra de firewall de nível de servidor em vez de uma regra de firewall de nível de banco de dados
P. Os usuários de um banco de dados devem ser totalmente isolados de outro banco de dados?   
  Em caso afirmativo, conceda o acesso usando regras de firewall no nível de banco de dados. Isso evita o uso de regras de firewall de nível de servidor, que permitem o acesso através do firewall Olá tooall bancos de dados, reduzindo a profundidade de saudação do defesas.   
 
P. Os usuários do endereço de IP hello necessário tooall bancos de dados acessam?   
  Use o firewall de nível de servidor regras tooreduce hello, o número de vezes que você deve configurar as regras de firewall.   

P. Pessoa hello ou equipe Configurando regras de firewall Olá só tem acesso por meio de Olá do portal do Azure, PowerShell ou Olá API REST?   
  É necessário usar regras de firewall no nível de servidor. As regras de firewall no nível de banco de dados só podem ser configuradas com o Transact-SQL.  

P. Pessoa hello ou equipe Configurando regras de firewall de saudação é proibido de ter permissão de alto nível no nível de banco de dados Olá?   
  Use regras de firewall no nível de servidor. Configurando regras de firewall de nível de banco de dados usando o Transact-SQL, requer pelo menos `CONTROL DATABASE` permissão no nível de banco de dados de saudação.  

P. É a pessoa hello ou equipe auditoria regras de firewall hello, ou configurando gerenciar centralmente as regras de firewall para muitos (talvez 100) de bancos de dados?   
  Essa seleção depende de suas necessidades e do ambiente. Regras de firewall de nível de servidor podem ser mais fácil tooconfigure, mas o script pode configurar regras em Olá nível de banco de dados. E mesmo se você usar regras de firewall de nível de servidor, talvez seja necessário regras de firewall de banco de dados de saudação do tooaudit, toosee se os usuários com `CONTROL` permissão no banco de dados de saudação criou regras de firewall de nível de banco de dados.   

P. Posso usar uma combinação das regras de firewall no nível de servidor e de banco de dados?   
  Sim. Alguns usuários, como administradores, podem precisar de regras de firewall no nível de servidor. Outros usuários, como usuários de um aplicativo de banco de dados, podem precisar de regras de firewall no nível de banco de dados.   

## <a name="troubleshooting-hello-database-firewall"></a>Solucionando problemas do firewall do banco de dados de saudação
Considere Olá pontos a seguir ao fazer acesso toohello serviço de banco de dados SQL do Microsoft Azure não se comportar conforme o esperado:

* **Configuração de firewall local:** antes do computador pode acessar o banco de dados do SQL Azure, talvez seja necessário toocreate uma exceção de firewall no seu computador para a porta TCP 1433. Se você estiver fazendo conexões dentro do limite de nuvem do Azure hello, você pode ter tooopen de portas adicionais. Para obter mais informações, consulte Olá **banco de dados SQL: fora versus dentro de** seção [portas além 1433 para ADO.NET 4.5 e o banco de dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md).
* **Rede NAT (NAT):** tooNAT de vencimento, o endereço IP de saudação usado pelo seu tooAzure tooconnect de computador banco de dados SQL pode ser diferente do endereço IP hello mostrado nas configurações de configuração de IP do computador. endereço IP de saudação tooview seu computador está usando tooconnect tooAzure, faça logon no portal de toohello e navegue toohello **configurar** guia no servidor de saudação que hospeda seu banco de dados. Em Olá **endereços IP permitidos** seção, hello **endereço IP do cliente atual** é exibido. Clique em **adicionar** toohello **endereços IP permitidos** tooallow este servidor de saudação do computador tooaccess.
* **Lista de permissões toohello alterações não entraram em vigor ainda:** pode haver quanto um atraso de cinco minutos para efeito de tootake de configuração de firewall do toohello banco de dados SQL é alterado.
* **logon de saudação não está autorizado ou uma senha incorreta foi usada:** se um logon não tem permissões no servidor de banco de dados do Azure SQL hello ou Olá senha usada estiver incorreta, o servidor de banco de dados SQL do hello conexão toohello foi negado. Criar uma configuração de firewall apenas oferece aos clientes com uma tooattempt oportunidade conectando o servidor tooyour; cada cliente deve fornecer credenciais de segurança necessárias hello. Para saber mais sobre a preparação de logons, consulte Gerenciando bancos de dados, logons e usuários no Banco de Dados SQL do Azure.
* **Endereço IP dinâmico:** se você tiver uma conexão de Internet com endereçamento IP dinâmico e você estiver tendo dificuldades para atravessar o firewall hello, tente uma saudação soluções a seguir:
  
  * Peça ao seu provedor de serviço de Internet (ISP) para o intervalo de endereços IP hello atribuído tooyour computadores nesse servidor de banco de dados do Azure SQL Olá acesso e, em seguida, adicionar intervalo de endereços IP hello como uma regra de firewall.
  * Obter o endereçamento IP estático em vez disso, para seus computadores cliente e, em seguida, adicionar endereços IP hello como regras de firewall.

## <a name="next-steps"></a>Próximas etapas

- Para um início rápido sobre como criar um banco de dados e uma regra de firewall de nível de servidor, consulte [Criar um Banco de Dados SQL do Azure](sql-database-get-started-portal.md).
- Para obter ajuda no banco de dados do SQL Azure tooan conexão de fonte aberta ou aplicativos de terceiros, consulte [tooSQL banco de dados de exemplos de código de início rápido do cliente](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Para obter informações sobre portas adicionais que talvez você precise tooopen, consulte Olá **banco de dados SQL: fora versus dentro de** seção [portas além 1433 para ADO.NET 4.5 e o banco de dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md)
- Para obter uma visão geral de segurança do Banco de Dados SQL do Azure, consulte [Protegendo seu banco de dados](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
