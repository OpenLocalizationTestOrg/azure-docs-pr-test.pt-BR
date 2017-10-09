---
title: "problemas de conexão comuns aaaTroubleshoot tooAzure banco de dados SQL"
description: "Etapas tooidentify e resolver conexão erros comuns para o banco de dados do SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Solucionar problemas de conexão tooAzure banco de dados SQL
Quando a conexão de saudação tooAzure banco de dados SQL falha, você receberá [mensagens de erro](sql-database-develop-error-messages.md). Este artigo é um tópico centralizado que ajuda a solucionar problemas de conectividade do Banco de Dados SQL do Azure. Ele apresenta [Olá causas comuns](#cause) de problemas de conexão, recomenda [uma ferramenta de solução de problemas](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) que ajuda você a problema de saudação de identidade e fornece toosolve de etapas de solução de problemas [ erros transitórios](#troubleshoot-transient-errors) e [persistentes ou não transitório erros](#troubleshoot-persistent-errors). 

Se você encontrar problemas de conexão hello, tente Olá solucionar os passos descritos neste artigo.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Causa
Problemas de Conexão podem ser causados por qualquer uma das seguintes hello:

* Práticas recomendadas de tooapply falha e diretrizes de design durante o processo de design de aplicativo hello.  Consulte [visão geral do desenvolvimento de banco de dados SQL](sql-database-develop-overview.md) tooget iniciado.
* Reconfiguração do Banco de Dados SQL do Azure
* Configurações de firewall
* Tempo limite da conexão
* Informações de logon incorretas
* Limite máximo é atingido para alguns recursos do Banco de Dados SQL do Azure

Em geral, problemas de conexão tooAzure banco de dados SQL pode ser classificado da seguinte maneira:

* [Erros transitórios (de curta duração ou intermitentes)](#troubleshoot-transient-errors)
* [Erros persistentes ou não transitórios (erros regularmente recorrentes)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Tente Olá a solução de problemas para problemas de conectividade de banco de dados SQL
Se você se deparar com um erro de conexão específico, tente [esta ferramenta](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), que vai ajudá-lo a identificar e resolver rapidamente o problema.

## <a name="troubleshoot-transient-errors"></a>Solucionar problemas de erros transitórios

Quando um aplicativo se conecta tooan banco de dados do SQL Azure, você receberá Olá a seguinte mensagem de erro:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Essa mensagem de erro normalmente é transitória (de vida curta).
> 
> 

Esse erro ocorre quando hello banco de dados do Azure está sendo movido (ou reconfigurado) e o aplicativo perde seu banco de dados SQL de toohello de conexão. Eventos de reconfiguração do banco de dados SQL ocorrem devido a um evento planejado (por exemplo, um upgrade de software) ou um evento não planejado (por exemplo, uma falha no processo ou balanceamento de carga). A maioria dos eventos de reconfiguração geralmente é de curta duração e deve ser concluída em, no máximo, de 60 segundos. No entanto, esses eventos, ocasionalmente, podem levar mais toofinish, como quando uma transação faz com que a recuperação de longa execução.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Problemas de conectividade transitória tooresolve etapas

1. Verificar Olá [painel de serviço do Microsoft Azure](https://azure.microsoft.com/status) para quaisquer interrupções conhecidas que ocorreram durante o tempo de saudação durante o qual Olá erro foi relatado pelo aplicativo hello.
2. Aplicativos que se conectam tooa serviço em nuvem como banco de dados do SQL Azure deve esperar que os eventos de reconfiguração periódica e implementar novamente lógica toohandle esses erros em vez de adicionar esses como toousers de erros do aplicativo. Saudação de revisão [erros transitórios](sql-database-connectivity-issues.md) seção Olá práticas recomendadas e diretrizes em de design [visão geral do desenvolvimento de banco de dados SQL](sql-database-develop-overview.md) estratégias de repetição para obter mais informações e geral. Em seguida, confira os exemplos de código em [Bibliotecas de Conexões para Banco de Dados SQL e SQL Server](sql-database-libraries.md) para obter as especificações.
3. Como um banco de dados se aproximar seus limites de recurso, ele pode parecer toobe um problema de conectividade transitória. Confira [Solução de problemas de desempenho](sql-database-troubleshoot-performance.md).
4. Se continuam a problemas de conectividade ou se hello duração para as quais seu aplicativo encontrar erro Olá excede 60 segundos ou se você vir várias ocorrências do erro de saudação em um determinado dia, uma solicitação de suporte do Azure de arquivos selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors"></a>Solucionar erros persistentes
Se aplicativo hello persistentemente falhar tooconnect tooAzure banco de dados SQL, ele normalmente indica um problema com um dos seguintes hello:

* Configuração do firewall. firewall de banco de dados ou do lado do cliente do SQL Azure Hello está bloqueando conexões tooAzure banco de dados SQL.
* Reconfiguração do lado do cliente de saudação de rede: por exemplo, um novo endereço IP ou um servidor proxy.
* Erro do usuário: por exemplo, parâmetros de conexão, como o nome do servidor de saudação na cadeia de caracteres de conexão de saudação de erro de digitação.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Problemas de conectividade persistente tooresolve etapas
1. Configurar [as regras de firewall](sql-database-configure-firewall-settings.md) tooallow endereço IP do cliente de saudação. Para fins de teste temporárias, configure uma regra de firewall usando 0.0.0.0 como saudação inicial do intervalo de endereços IP e usando 255.255.255.255 como Olá final do intervalo de endereços IP. Isso abrirá Olá tooall endereços IP. Se isso resolver seu problema de conectividade, remova essa regra e crie uma regra de firewall para um intervalo de endereçamento ou um endereço IP adequadamente limitado. 
2. Em todos os firewalls entre o cliente hello e hello da Internet, certifique-se de que a porta 1433 está aberta para conexões de saída. Revisão [configurar o Firewall do Windows de saudação tooAllow acesso ao SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) e [protocolos e portas necessárias de identidade híbrida](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) para ponteiros adicionais relacionadas tooadditional portas que você precisa tooopen para Autenticação do Active Directory do Azure.
3. Verifique a cadeia de conexão e outras configurações de conexão. Consulte Olá seção da cadeia de caracteres de Conexão no hello [tópico de problemas de conectividade](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Verifique a integridade do serviço no painel de saudação. Se você acha que houver uma interrupção regional, consulte [recuperar de uma paralisação](sql-database-disaster-recovery.md) para nova região de etapas toorecover tooa.

## <a name="next-steps"></a>Próximas etapas
* [Solucionar problemas de desempenho no Banco de Dados SQL do Azure](sql-database-troubleshoot-performance.md)
* [Documentação de saudação de pesquisa no Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Saudação de exibição atualizações mais recentes toohello serviço de banco de dados SQL](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Recursos adicionais
* [Visão geral do desenvolvimento de Banco de Dados SQL](sql-database-develop-overview.md)
* [Diretrizes gerais para tratamento de falhas transitórias](../best-practices-retry-general.md)
* [Bibliotecas de conexão para Banco de Dados SQL e SQL Server](sql-database-libraries.md)

