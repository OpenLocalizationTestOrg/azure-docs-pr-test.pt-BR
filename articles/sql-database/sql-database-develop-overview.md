---
title: "Visão geral do desenvolvimento de aplicativo de banco de dados de aaaSQL | Microsoft Docs"
description: "Saiba mais sobre as bibliotecas de conectividade disponível e práticas recomendadas para aplicativos que se conectam tooSQL banco de dados."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Visão geral do desenvolvimento de aplicativos de Banco de Dados SQL
Este artigo explica considerações básicas de saudação que um desenvolvedor deve estar atento ao escrever código tooconnect tooAzure banco de dados SQL.

> [!TIP]
> Para um tutorial mostrando você como toocreate um servidor, criar um firewall baseado em servidor, exibir propriedades do servidor, conecte-se usando o SQL Server Management Studio, o banco de dados mestre de saudação de consulta, crie um banco de dados de exemplo e um banco de dados em branco, consulta propriedades de banco de dados, conecte-se usando o SQL Server Management Studio e o banco de dados de exemplo de hello consulta, consulte [obter Tutorial de Introdução](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Linguagem e plataforma
Há exemplos de código disponíveis para uma variedade de plataformas e linguagens de programação. Você pode encontrar exemplos de código toohello links em: 

* Mais informações: [bibliotecas de conexão para Banco de Dados SQL e SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Ferramentas 
Você pode aproveitar as ferramentas de software livre, como [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [Código VS](https://code.visualstudio.com/). Além disso, o Banco de Dados SQL do Azure funciona com ferramentas da Microsoft, como [Visual Studio](https://www.visualstudio.com/downloads/) e [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  Você também pode usar o hello Portal de gerenciamento do Azure PowerShell, e APIs REST ajudarão a aumentar a produtividade adicional.

## <a name="resource-limitations"></a>Limitações de recursos
Banco de dados SQL do Azure gerencia Olá recursos disponíveis tooa banco de dados usando dois mecanismos diferentes: governança de recursos e a imposição de limites.

* Mais informações: [limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md)

## <a name="security"></a>Segurança
O Banco de Dados SQL do Azure fornece recursos para limitar o acesso, proteger os dados e monitorar atividades em um Banco de Dados SQL.

* Mais informações: [proteger seu Banco de Dados SQL](sql-database-security-overview.md)

## <a name="authentication"></a>Autenticação
* O Banco de Dados SQL do Azure permite logons e usuários da autenticação do SQL Server, bem como usuários e logons da [autenticação do Azure Active Directory](sql-database-aad-authentication.md) .
* É necessário toospecify um determinado banco de dados, em vez de uso padrão toohello *mestre* banco de dados.
* Você não pode usar o Transact-SQL de saudação **myDatabaseName uso;** instrução no banco de dados do banco de dados SQL tooswitch tooanother.
* Mais informações: [segurança do Banco de Dados SQL: gerenciar o acesso ao banco de dados e a segurança de logon](sql-database-manage-logins.md)

## <a name="resiliency"></a>Resiliência
Quando ocorre um erro temporário durante a conexão tooSQL banco de dados, seu código deverá repetir a chamada de saudação.  É recomendável que a lógica de repetição usar lógica de retirada, para que ele não sobrecarregar Olá banco de dados SQL com vários clientes simultaneamente repetir.

* Exemplos de código: para exemplos de código que ilustram a lógica de repetição, consulte exemplos para o idioma de saudação de sua preferência em: [bibliotecas de Conexão para o banco de dados SQL e SQL Server](sql-database-libraries.md)
* Mais informações: [Mensagens de erro para programas cliente do Banco de Dados SQL](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Gerenciando conexões
* Em sua lógica de conexão de cliente, substitua toobe de tempo limite padrão Olá 30 segundos.  padrão de saudação de 15 segundos é muito pequeno para conexões que dependem Olá da internet.
* Se você estiver usando um [pool de conexão](http://msdn.microsoft.com/library/8xx3tyca.aspx), se tooclose Olá Olá de conexão instantânea seu programa não está sendo ativamente usada e não está preparando tooreuse-lo.

## <a name="network-considerations"></a>Considerações sobre rede
* No computador de saudação que hospeda o programa cliente, certifique-se de saudação firewall permite a comunicação TCP de saída na porta 1433.  Mais informações: [Configurar um firewall de Banco de Dados SQL do Azure](sql-database-configure-firewall-settings.md)
* Se seu programa cliente conecta-se tooSQL banco de dados enquanto o cliente é executado em uma máquina virtual do Azure (VM), você deve abrir determinados intervalos de porta Olá VM. Mais informações: [Portas além da 1433 para ADO.NET 4.5 e Banco de Dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md)
* Conexões de cliente tooAzure banco de dados SQL, às vezes, ignorar proxy hello e interagir diretamente com o banco de dados de saudação. Outras portas diferentes da 1433 se tornam importantes. Para obter mais informações, [Arquitetura de conectividade de Banco de Dados SQL do Azure](sql-database-connectivity-architecture.md) e [Portas além da 1433 para ADO.NET 4.5 e Banco de Dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Fragmentação de dados com escala elástica
Escala elástica simplifica o processo de saudação do dimensionamento de saída (e em). 

* [Padrões de design para aplicativos SaaS multilocatários com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md)
* [Introdução à visualização da Escala Elástica do Banco de Dados SQL do Azure](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Próximas etapas
Explorar todos os Olá [recursos do banco de dados SQL](sql-database-technical-overview.md)
