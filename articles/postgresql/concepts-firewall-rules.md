---
title: Regras de firewall do Banco de Dados do Azure para servidor PostgreSQL | Microsoft Docs
description: Descreve as regras de firewall para seu Banco de Dados do Azure para servidor PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Regras de firewall do Banco de Dados do Azure para servidor PostgreSQL
Firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede servidor toohello de acesso com base em Olá endereços IP de cada solicitação de origem.
tooconfigure seu firewall, criar regras de firewall que especifiquem intervalos de endereços IP aceitáveis. Você pode criar regras de firewall no nível do servidor de saudação.

**Regras de firewall:** essas regras permitem que os clientes tooaccess seu banco de dados inteiro do Azure para o servidor PostgreSQL, ou seja, todos os bancos de dados de saudação em Olá mesmo servidor lógico. Regras de firewall de nível de servidor podem ser configuradas usando Olá portal do Azure ou usando os comandos de CLI do Azure. regras de firewall no nível de servidor toocreate, você deve ser o proprietário da assinatura hello ou um colaborador da assinatura.

## <a name="firewall-overview"></a>Visão geral do firewall
Todos os tooyour de acesso de banco de dados banco de dados PostgreSQL servidor seja bloqueada pelo firewall do hello por padrão. toobegin usando o servidor a partir de outro computador, você precisa toospecify um servidor ou de nível de servidor mais firewall regras tooenable acesso tooyour. Use toospecify de regras de firewall Olá qual endereço IP varia de saudação Internet tooallow. Acesso toohello site do portal do Azure em si não é afetada por regras de firewall de saudação.
Olá de tentativas de Conexão de Internet e o Azure deve passar primeiramente pelo firewall Olá antes de poderem acessar o banco de dados PostgreSQL, conforme mostrado no diagrama a seguir de saudação:

![Fluxo de exemplo de como funciona o firewall Olá](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Conectando-se de saudação da Internet
Regras de firewall de nível de servidor aplicam bancos de dados tooall hello banco de dados do Azure para servidor PostgreSQL. Se Olá endereço IP de saudação solicitação estiver dentro de um dos intervalos de saudação especificados nas regras de firewall de nível de servidor de saudação, conexão Olá será concedida.
Se Olá endereço IP de saudação solicitação não está dentro de intervalos de saudação especificado em qualquer Olá nível de banco de dados ou regras de firewall no nível de servidor, falha de solicitação de conexão de saudação.
Por exemplo, se seu aplicativo se conecta ao driver JDBC para PostgreSQL, você pode encontrar esse erro tentar tooconnect quando Olá firewall está bloqueando a conexão de saudação.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Gerenciando programaticamente as regras de firewall
Além disso, toohello portal do Azure, firewall, regras podem ser gerenciadas programaticamente usando a CLI do Azure.
Confira também [Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Solucionando problemas do firewall do banco de dados de saudação
Considere Olá pontos a seguir ao fazer acesso toohello banco de dados do Microsoft Azure para o serviço de servidor PostgreSQL não se comportar conforme o esperado:

* **Lista de permissões toohello alterações não entraram em vigor ainda:** pode haver quanto um atraso de cinco minutos para alterações toohello banco de dados do Azure para efeito de tootake de configuração de firewall de servidor PostgreSQL.

* **logon de saudação não está autorizado ou uma senha incorreta foi usada:** se um logon não tiver permissões no hello banco de dados PostgreSQL server ou hello senha usada é incorreta, Olá conexão toohello banco de dados do Azure para servidor PostgreSQL é negado. Criar uma configuração de firewall apenas oferece aos clientes com uma tooattempt oportunidade conectando o servidor tooyour; cada cliente deve fornecer credenciais de segurança necessárias hello.

Por exemplo, usando um cliente JDBC, Olá erro a seguir pode aparecer.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: falha na autenticação da senha para o usuário "seunomedeusuário"

* **Endereço IP dinâmico:** se você tiver uma conexão de Internet com endereçamento IP dinâmico e você estiver tendo dificuldades para atravessar o firewall hello, tente uma saudação soluções a seguir:

* Peça ao seu provedor de serviço de Internet (ISP) para o intervalo de endereços IP hello atribuídos tooyour os computadores cliente que Olá acesso banco de dados PostgreSQL servidor e, em seguida, adicionar intervalo de endereços IP hello como uma regra de firewall.

* Obter o endereçamento IP estático em vez disso, para seus computadores cliente e, em seguida, adicionar endereços IP hello como regras de firewall.

## <a name="next-steps"></a>Próximas etapas
Para ver artigos sobre como criar regras de firewall no nível de servidor e de banco de dados, consulte:
* [Criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure](howto-manage-firewall-using-portal.md)
* [Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure](howto-manage-firewall-using-cli.md)