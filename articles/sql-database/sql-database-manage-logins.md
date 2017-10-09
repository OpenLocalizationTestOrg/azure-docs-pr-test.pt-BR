---
title: "aaaAzure SQL logons e usuários | Microsoft Docs"
description: "Saiba mais sobre o gerenciamento de segurança de banco de dados SQL, especificamente como toomanage banco de dados segurança de logon e acesso por meio da conta de entidade de nível de servidor de saudação."
keywords: "segurança do banco de dados SQL, gerenciamento de segurança de banco de dados, segurança de logon, segurança de banco de dados, acesso ao banco de dados"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Controle e concessão de acesso de banco de dados

Quando as regras de firewall foi configuradas, as pessoas podem se conectar tooa banco de dados SQL como uma saudação contas de administrador, como proprietário do banco de dados de saudação ou como um usuário de banco de dados no banco de dados de saudação.  

>  [!NOTE]  
>  Este tópico se aplica a tooAzure SQL server e tooboth banco de dados SQL e SQL Data Warehouse bancos de dados que são criados no servidor do SQL Azure hello. Para simplificar, banco de dados SQL é usado ao fazer referência tooboth banco de dados SQL e SQL Data Warehouse. 
>

> [!TIP]
> Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Contas administrativas irrestritas
Há duas contas administrativas (**Administrador do servidor** e **Administrador do Active Directory**) que agem como administradores. tooidentify essas contas de administrador do SQL server, abra Olá portal do Azure e navegue toohello propriedades do SQL server.

![Administradores do SQL Server](./media/sql-database-manage-logins/sql-admins.png)

- **Administrador do servidor**   
Quando você cria um servidor SQL no Azure, você deve designar um **Logon de administrador do servidor**. SQL server cria essa conta como um logon no banco de dados mestre hello. Essa conta é conectada usando a autenticação do SQL Server (nome de usuário e senha). Só pode existir uma dessas contas.   
- **Administrador do Azure Active Directory**   
Uma conta do Azure Active Directory, seja ela individual ou de grupo de segurança, também pode ser configurada como um administrador. É opcional tooconfigure um administrador do AD do Azure, mas um administrador do AD do Azure deve ser configurado se você quiser toouse AD do Azure contas tooconnect tooSQL banco de dados. Para obter mais informações sobre como configurar o acesso do Active Directory do Azure, consulte [tooSQL conectando banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](sql-database-aad-authentication.md) e [SSMS suporte para MFA do Azure AD com SQL Banco de dados e SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).
 

Olá **administrador do servidor** e **admin do AD do Azure** contas tem Olá características a seguir:
- Esses são Olá somente as contas que podem se conectar automaticamente a tooany banco de dados SQL no servidor de saudação. (dados de usuário de tooa tooconnect, outras contas devem ser proprietário de saudação de saudação do banco de dados ou ter uma conta de usuário no banco de dados de usuário hello.)
- Essas contas insiram bancos de dados de usuário como Olá `dbo` usuário e têm todas as permissões de saudação em bancos de dados de usuário de saudação. (proprietário de saudação de um banco de dados de usuário também insere o banco de dados de saudação como Olá `dbo` usuário.) 
- Essas contas não insira Olá `master` banco de dados como Olá `dbo` usuário e eles têm permissões limitadas no mestre. 
- Essas contas não são membros de saudação padrão do SQL Server `sysadmin` função de servidor fixa, que não está disponível no banco de dados SQL.  
- Essas contas podem criar, alterar e remover bancos de dados, logons, usuários nas regras de firewall mestre e de nível de servidor.
- Essas contas podem adicionar e remover membros toohello `dbmanager` e `loginmanager` funções.
- Essas contas podem visualizar Olá `sys.sql_logins` tabela do sistema.

### <a name="configuring-hello-firewall"></a>Configurando o firewall Olá
Quando o firewall no nível de servidor Olá estiver configurado para um endereço IP ou intervalo individual, Olá **administrador do SQL server** e hello **administrador do Active Directory do Azure** pode se conectar a banco de dados mestre toohello e hello todos os bancos de dados do usuário. Olá inicial firewall de nível de servidor pode ser configurado por meio de saudação [portal do Azure](sql-database-get-started-portal.md)usando [PowerShell](sql-database-get-started-powershell.md) ou usando Olá [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Depois que uma conexão é estabelecida, as regras de firewall adicionais no nível do servidor também podem ser configuradas usando o [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Caminho de acesso do administrador
Quando o firewall de nível de servidor de saudação está configurado corretamente, Olá **administrador do SQL server** e hello **administrador do Active Directory do Azure** podem se conectar usando as ferramentas de cliente, como o SQL Server Management Studio ou SQL Ferramentas de dados do servidor. Somente ferramentas mais recentes da saudação fornecem todos os recursos de saudação e recursos. Olá diagrama a seguir mostra uma configuração típica de saudação duas contas de administrador.

![Caminho de acesso do administrador](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Ao usar uma porta aberta no firewall de nível de servidor de saudação, os administradores podem se conectar tooany banco de dados SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Conexão tooa banco de dados usando o SQL Server Management Studio
Para obter instruções de criação de um servidor, um banco de dados, as regras de firewall de nível de servidor e usando o SQL Server Management Studio tooquery um banco de dados, consulte [começar com os servidores de banco de dados SQL, bancos de dados e as regras de firewall usando Olá portal do Azure e o SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Funções administrativas no nível do servidor adicionais
Além de funções de administrativas de nível de servidor toohello discutidas anteriormente, banco de dados SQL fornece duas funções administrativas restritas em contas de usuário de toowhich Olá banco de dados mestre podem ser adicionadas que conceda permissões tooeither criar bancos de dados ou gerenciar logons.

### <a name="database-creators"></a>Criadores de Banco de Dados
Uma dessas funções administrativas é hello **dbmanager** função. Os membros dessa função podem criar novos bancos de dados. toouse essa função, você cria um usuário no hello `master` banco de dados e, em seguida, adicionar Olá usuário toohello **dbmanager** função de banco de dados. toocreate um banco de dados, usuário Olá deve ser um usuário com base em um logon do SQL Server no banco de dados mestre hello ou contidos usuário de banco de dados com base em um usuário do Active Directory do Azure.

1. Usando uma conta de administrador, conecte-se toohello banco de dados mestre.
2. Etapa opcional: criar um logon de autenticação do SQL Server, usando Olá [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) instrução. Exemplo de instrução:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Você deve usar uma senha forte ao criar um logon ou um usuário de banco de dados independente. Para obter mais informações, consulte [Senhas fortes (a página pode estar em inglês)](https://msdn.microsoft.com/library/ms161962.aspx).
    
   tooimprove desempenho, logons (entidades de nível de servidor) são armazenados em cache temporariamente no nível de banco de dados de saudação. cache de autenticação Olá toorefresh, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. No banco de dados mestre hello, crie um usuário usando Olá [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) instrução. usuário Olá pode ser o usuário de banco de dados de autenticação contido Active Directory do Azure (se você tiver configurado o ambiente para a autenticação do AD do Azure), ou um usuário de banco de dados do SQL Server authentication contido ou um usuário de autenticação do SQL Server com base em um SQL Logon de autenticação de servidor (criado na etapa anterior hello.) Exemplo de instruções:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Adicionar novo usuário hello, toohello **dbmanager** função de banco de dados usando Olá [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instrução. Exemplo de instruções:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Olá dbmanager é uma função de banco de dados no banco de dados mestre para que você só pode adicionar uma função dbmanager de toohello de usuário de banco de dados. Não é possível adicionar uma função de nível toodatabase de logon de nível de servidor.
    
5. Se necessário, configure um firewall regra tooallow Olá novo usuário tooconnect. (novo usuário de saudação pode estar incluído em uma regra de firewall existente.)

Agora o usuário Olá pode se conectar toohello banco de dados mestre e pode criar novos bancos de dados. conta Olá criando Olá banco de dados se torna o proprietário de saudação do banco de dados de saudação.

### <a name="login-managers"></a>Gerentes de logon
Olá, outros função administrativa é gerente de logon hello. Os membros desta função podem criar novos logons no banco de dados mestre hello. Se desejar, você poderá concluir Olá mesmas etapas (criar um logon e usuário e adicionar um usuário toohello **loginmanager** função) tooenable um usuário toocreate novos logons no mestre de saudação. Geralmente os logons não são necessários como a Microsoft recomenda usar usuários do banco de dados independente, o que autenticam no hello-nível banco de dados em vez de usar usuários baseados em logons. Para obter mais informações, consulte [Usuários do banco de dados independente - Tornando o banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Usuários não administradores
Em geral, as contas de usuário não administrador não precisará de acesso toohello banco de dados mestre. Criar usuários de banco de dados independente no nível de banco de dados de saudação usando Olá [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instrução. usuário Olá pode ser o usuário de banco de dados de autenticação contido Active Directory do Azure (se você tiver configurado o ambiente para a autenticação do AD do Azure), ou um usuário de banco de dados do SQL Server authentication contido ou um usuário de autenticação do SQL Server com base em um SQL Logon de autenticação de servidor (criado na etapa anterior hello.) Para obter mais informações, consulte [Usuários do banco de dados independente - Tornando o banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx). 

usuários toocreate, conecte-se o banco de dados toohello e execute instruções toohello semelhante exemplos a seguir:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Inicialmente, apenas um dos administradores de saudação ou proprietário de saudação do banco de dados de saudação pode criar usuários. tooauthorize usuários adicionais toocreate novos usuários, conceder esse saudação do usuário selecionado `ALTER ANY USER` permissão, usando uma instrução, como:

```
GRANT ALTER ANY USER tooMary;
```

toogive usuários adicionais controle total do banco de dados hello, torná-los um membro da saudação **db_owner** função de banco de dados fixa usando Olá `ALTER ROLE` instrução.

> [!NOTE]
> Hello mais comuns motivo toocreate banco de dados de usuários com base em logons, é quando você tiver usuários de autenticação do SQL Server que precisam acessar bancos de dados de toomultiple. Usuários baseados em logons são logon toohello associado e apenas uma senha que é mantida para aquele logon. Os usuários do banco de dados independente em bancos de dados individuais são cada entidade individual, e cada uma delas mantém sua própria senha. Isso pode confundir os usuários de banco de dados independente se eles não mantiverem suas senhas idênticas.

### <a name="configuring-hello-database-level-firewall"></a>Configuração de firewall no nível de banco de dados Olá
Como uma prática recomendada, os usuários não administradores só devem ter acesso por meio de bancos de dados do hello firewall toohello que eles usam. Em vez de autorizar seu IP endereços por meio de nível de servidor de saudação do firewall e lhes conceder acesso a bancos de dados de tooall, use Olá [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) firewall no nível de banco de dados instrução tooconfigure hello. firewall de nível de banco de dados de saudação não pode ser configurado usando o portal de saudação.

### <a name="non-administrator-access-path"></a>Caminho de acesso do não administrador
Quando o firewall no nível de banco de dados hello está configurado corretamente, os usuários de banco de dados de saudação podem se conectar usando as ferramentas de cliente como o SQL Server Management Studio ou o SQL Server Data Tools. Somente ferramentas mais recentes da saudação fornecem todos os recursos de saudação e recursos. Olá diagrama a seguir mostra um caminho de acesso típico de não administrador.

![Caminho de acesso do não administrador](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Grupos e funções
Gerenciamento de acesso eficiente usa permissões atribuídas toogroups e funções em vez de usuários individuais. 

- Ao usar a autenticação do Azure Active Directory, coloque os usuários do Azure Active Directory em um grupo do Azure Active Directory. Crie um usuário de banco de dados independente para o grupo de saudação. Colocar um ou mais usuários de banco de dados em um [função de banco de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribuir [permissões](https://msdn.microsoft.com/library/ms191291.aspx) toohello função de banco de dados.

- Ao usar a autenticação do SQL Server, crie usuários de banco de dados contido no banco de dados de saudação. Colocar um ou mais usuários de banco de dados em um [função de banco de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribuir [permissões](https://msdn.microsoft.com/library/ms191291.aspx) toohello função de banco de dados.

funções de banco de dados de saudação podem ser funções internas hello como **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, e **db_denydatareader**. **db_owner** é comumente usados toogrant permissão total tooonly alguns poucos usuários. Olá outras funções fixas de banco de dados são úteis para a obtenção de um banco de dados simple em desenvolvimento rapidamente, mas não são recomendadas para a maioria dos bancos de dados de produção. Por exemplo, Olá **db_datareader** função de banco de dados fixa concede acesso de leitura tooevery tabela no banco de dados de saudação, que normalmente é maior que é estritamente necessária. É muito melhor Olá de toouse [Criar função](https://msdn.microsoft.com/library/ms187936.aspx) toocreate de instrução seus próprios definida pelo usuário funções de banco de dados e conceder cuidadosamente Olá cada função menos as permissões necessárias para Olá necessidade de negócios. Quando um usuário é um membro de várias funções, permissões de saudação de todas elas de agregação.

## <a name="permissions"></a>Permissões
Há mais de 100 permissões que podem ser concedidas ou negadas individualmente no Banco de Dados SQL. Muitas dessas permissões são aninhadas. Por exemplo, Olá `UPDATE` permissão em um esquema inclui Olá `UPDATE` permissão em cada tabela no esquema. Como a maioria dos sistemas de permissão, Olá negação uma permissão substitui uma concessão. Devido à natureza de saudação aninhada e número de saudação de permissões, pode levar cuidado estudo toodesign tooproperly de sistema uma permissão apropriada proteger seu banco de dados. Começar com hello lista de permissões em [permissões (mecanismo de banco de dados)](https://msdn.microsoft.com/library/ms191291.aspx) e examine Olá [gráfico do cartaz tamanho](http://go.microsoft.com/fwlink/?LinkId=229142) de permissões de saudação.


### <a name="considerations-and-restrictions"></a>Considerações e restrições
Ao gerenciar logons e usuários no banco de dados SQL, considere o seguinte hello:

* Você deve ser conectado toohello **mestre** banco de dados ao executar Olá `CREATE/ALTER/DROP DATABASE` instruções.   
* Olá toohello correspondente do usuário de banco de dados **administrador do servidor** logon não pode ser alterado ou descartado. 
* Inglês é o idioma de padrão de saudação do hello **administrador do servidor** logon.
* Olá somente administradores (**administrador do servidor** login ou o administrador do AD do Azure) e os membros de saudação da saudação **dbmanager** função de banco de dados em hello **mestre** tem do banco de dados saudação de tooexecute permissão `CREATE DATABASE` e `DROP DATABASE` instruções.
* Deve ser o banco de dados mestre toohello conectado ao executar Olá `CREATE/ALTER/DROP LOGIN` instruções. No entanto, não é recomendado usar logons. Utilize os usuários de bancos de dados independentes.
* tooconnect tooa de dados de usuário, você deve fornecer o nome de saudação do banco de dados de saudação na cadeia de caracteres de conexão de saudação.
* Olá apenas o nível de servidor principal logon e hello membros de saudação **loginmanager** função de banco de dados em Olá **mestre** banco de dados ter Olá de tooexecute permissão `CREATE LOGIN`, `ALTER LOGIN`, e `DROP LOGIN` instruções.
* Ao executar Olá `CREATE/ALTER/DROP LOGIN` e `CREATE/ALTER/DROP DATABASE` instruções em um aplicativo ADO.NET, usar comandos parametrizados não é permitido. Para obter mais informações, veja [Comandos e parâmetros](https://msdn.microsoft.com/library/ms254953.aspx).
* Ao executar Olá `CREATE/ALTER/DROP DATABASE` e `CREATE/ALTER/DROP LOGIN` instruções, cada uma dessas instruções deve ser Olá apenas uma instrução em um lote de Transact-SQL. Caso contrário, ocorrerá um erro. Por exemplo, hello que Transact-SQL a seguir verifica se o banco de dados de saudação existe. Se ele existir, um `DROP DATABASE` instrução é chamada de banco de dados do tooremove hello. Porque Olá `DROP DATABASE` instrução não for Olá única instrução no lote hello, executando Olá seguinte instrução Transact-SQL resulta em um erro.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Ao executar Olá `CREATE USER` instrução com hello `FOR/FROM LOGIN` opção, ele deve ser Olá apenas uma instrução em um lote de Transact-SQL.
* Ao executar Olá `ALTER USER` instrução com hello `WITH LOGIN` opção, ele deve ser Olá apenas uma instrução em um lote de Transact-SQL.
* muito`CREATE/ALTER/DROP` requer que um usuário Olá `ALTER ANY USER` permissão no banco de dados de saudação.
* Quando o proprietário de saudação de uma função de banco de dados tenta tooadd ou remover outro tooor de usuário de banco de dados da função de banco de dados, Olá erro a seguir pode ocorrer: **usuário ou função 'Name' não existe neste banco de dados.** Esse erro ocorre porque o usuário Olá não é proprietário toohello visível. tooresolve esse problema, conceda Olá Olá de proprietário de função `VIEW DEFINITION` permissão no usuário hello. 


## <a name="next-steps"></a>Próximas etapas

- toolearn mais informações sobre regras de firewall, consulte [Firewall de banco de dados do SQL Azure](sql-database-firewall-configure.md).
- Para obter uma visão geral de todos os recursos de segurança do banco de dados SQL hello, consulte [visão geral de segurança do SQL](sql-database-security-overview.md).
- Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).
- Para saber mais sobre exibições e procedimentos armazenados, veja [Criação de exibições e procedimentos armazenados](https://msdn.microsoft.com/library/ms365311.aspx)
- Para obter informações sobre como conceder o objeto de banco de dados do access tooa, consulte [tooa concedendo acesso a objeto de banco de dados](https://msdn.microsoft.com/library/ms365327.aspx)
