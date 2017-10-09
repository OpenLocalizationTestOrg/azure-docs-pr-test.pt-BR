---
title: aaaAzure banco de dados MySQL server para regras de firewall | Microsoft Docs
description: Descreve as regras de firewall para seu Banco de Dados do Azure para servidor MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>Regras de firewall do Banco de Dados do Azure para servidor MySQL
Firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede servidor toohello de acesso com base em Olá endereços IP de cada solicitação de origem.

tooconfigure seu firewall, criar regras de firewall que especifiquem intervalos de endereços IP aceitáveis. Você pode criar regras de firewall no nível do servidor de saudação.

**Regras de firewall:** essas regras permitem que os clientes tooaccess seu banco de dados inteiro do Azure para o MySQL server, ou seja, todos os bancos de dados de saudação em Olá mesmo servidor lógico. Regras de firewall de nível de servidor podem ser configuradas usando Olá portal do Azure ou usando os comandos de CLI do Azure. regras de firewall no nível de servidor toocreate, você deve ser o proprietário da assinatura hello ou um colaborador da assinatura.

## <a name="firewall-overview"></a>Visão geral do firewall
Todos os tooyour de acesso de banco de dados banco de dados do Azure para o MySQL server está bloqueado pelo firewall do hello por padrão. toobegin usando o servidor a partir de outro computador, você precisa toospecify um servidor ou de nível de servidor mais firewall regras tooenable acesso tooyour. Use toospecify de regras de firewall Olá qual endereço IP varia de saudação Internet tooallow. Acesso toohello site do portal do Azure em si não é afetada por regras de firewall de saudação.

Olá de tentativas de Conexão de Internet e o Azure deve passar primeiramente pelo firewall Olá antes de poderem acessar o banco de dados do Azure para o banco de dados MySQL, conforme mostrado no diagrama a seguir de saudação:

![Fluxo de exemplo de como funciona o firewall Olá](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Conectando-se de saudação da Internet
Regras de firewall de nível de servidor aplicam bancos de dados tooall hello banco de dados para o servidor MySQL.

Se Olá endereço IP de saudação solicitação estiver dentro de um dos intervalos de saudação especificados nas regras de firewall de nível de servidor de saudação, conexão Olá será concedida.

Se Olá endereço IP de saudação solicitação não está dentro de intervalos de saudação especificado em qualquer Olá nível de banco de dados ou regras de firewall no nível de servidor, falha de solicitação de conexão de saudação.

## <a name="programmatically-managing-firewall-rules"></a>Gerenciando programaticamente as regras de firewall
Além disso, toohello portal do Azure, firewall, regras podem ser gerenciadas programaticamente usando a CLI do Azure. Confira também [Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando a CLI do Azure](./howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Solucionando problemas do firewall do banco de dados de saudação
Considere Olá pontos a seguir ao fazer acesso toohello banco de dados do Microsoft Azure para o serviço do servidor MySQL não se comportar conforme o esperado:

* **Lista de permissões toohello alterações não entraram em vigor ainda:** pode haver quanto um atraso de cinco minutos para alterações toohello banco de dados do Azure para efeito de tootake de configuração de firewall de servidor MySQL.

* **logon de saudação não está autorizado ou uma senha incorreta foi usada:** se um logon não tiver permissões no hello banco de dados MySQL server ou hello senha usada é incorreta, Olá conexão toohello banco de dados para o servidor MySQL foi negado. Criar uma configuração de firewall apenas oferece aos clientes com uma tooattempt oportunidade conectando o servidor tooyour; cada cliente deve fornecer credenciais de segurança necessárias hello.

* **Endereço IP dinâmico:** se você tiver uma conexão de Internet com endereçamento IP dinâmico e você estiver tendo dificuldades para atravessar o firewall hello, tente uma saudação soluções a seguir:

* Peça ao seu provedor de serviço de Internet (ISP) para o intervalo de endereços IP hello atribuído tooyour os computadores cliente que Olá acesso banco de dados do Azure para o MySQL server e, em seguida, adicionar intervalo de endereços IP hello como uma regra de firewall.

* Obter o endereçamento IP estático em vez disso, para seus computadores cliente e, em seguida, adicionar endereços IP hello como regras de firewall.

## <a name="next-steps"></a>Próximas etapas

[Criar e gerenciar o banco de dados MySQL para regras de firewall usando o portal do Azure de saudação](./howto-manage-firewall-using-portal.md)
[criar e gerenciar o banco de dados MySQL para regras de firewall usando a CLI do Azure](./howto-manage-firewall-using-cli.md)
