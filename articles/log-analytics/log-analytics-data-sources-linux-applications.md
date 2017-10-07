---
title: "aaaCollect Linux o desempenho do aplicativo na análise de logs do OMS | Microsoft Docs"
description: "Este artigo fornece detalhes para a configuração de saudação do agente do OMS para contadores de desempenho do Linux toocollect para o Apache HTTP Server e MySQL."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Coletar contadores de desempenho para aplicativos Linux no Log Analytics 
Este artigo fornece detalhes de configuração Olá [agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect contadores de desempenho para aplicativos específicos.  Olá aplicativos incluídos neste artigo são:  

- [MySQL](#MySQL)
- [Apache HTTP Server](#apache-http-server)

## <a name="mysql"></a>MySQL
Se o servidor MySQL ou MariaDB for detectado no computador de saudação quando o agente do OMS Olá é instalado, um provedor para o MySQL Server de monitoramento de desempenho será instalado automaticamente. Esse provedor se conecta toohello local MySQL/MariaDB tooexpose desempenho estatísticas do servidor. As credenciais de usuário do MySQL devem ser configuradas para que hello provedor possa acessar saudação do MySQL Server.

### <a name="configure-mysql-credentials"></a>Configurar as credenciais do MySQL
Hello provedor de OMI do MySQL requer um usuário do MySQL pré-configurado e bibliotecas de cliente de MySQL instaladas na ordem tooquery Olá informações de desempenho e integridade da instância do MySQL hello.  Essas credenciais são armazenadas em um arquivo de autenticação que é armazenado no agente do Linux hello.  arquivo de autenticação de saudação especifica o endereço de associação e porta Olá MySQL instância está escutando e quais credenciais toouse toogather métricas.  

Durante a instalação de saudação do agente do OMS para Linux Olá OMI do MySQL provedor verificar arquivos de configuração my.cnf do MySQL (locais padrão) para o endereço de associação e a porta e parcialmente conjunto Olá arquivo de autenticação de OMI do MySQL.

arquivo de autenticação do MySQL Olá é armazenado em `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Formato do arquivo de autenticação
É o formato de saudação para Olá arquivo de autenticação de OMI do MySQL

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

entradas de saudação no arquivo de autenticação Olá são descritas na Olá a tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| Porta | Representa Olá Olá atual da porta escuta da instância do MySQL. Porta 0 especifica que propriedades de saudação a seguir são usadas para a instância padrão. |
| Endereço de Ligação| Endereço de associação atual de MySQL. |
| Nome de Usuário| Usuário do MySQL usado instância do servidor toouse toomonitor Olá MySQL. |
| Senha codificada em Base64| Senha do usuário monitoramento do MySQL Olá codificada em Base64. |
| Atualização Automática| Especifica se toorescan para as alterações no arquivo my.cnf de saudação e substituir o arquivo de autenticação de OMI do MySQL hello quando hello provedor de OMI do MySQL é atualizado. |

### <a name="default-instance"></a>Instância padrão
Olá arquivo de autenticação de OMI do MySQL pode definir uma instância padrão e toomake de número de porta gerenciar várias instâncias do MySQL em um host Linux mais fácil.  instância padrão de saudação é indicada por uma instância com a porta 0. Todas as instâncias adicionais herdarão as propriedades definidas da instância de padrão de saudação, a menos que elas especificam valores diferentes. Por exemplo, se a instância do MySQL escutando na porta '3308' for adicionada, endereço de associação da instância de saudação padrão, nome de usuário e senha codificada em Base64 serão ser tootry usado e monitorar Olá instância escuta na porta 3308. Se instância Olá em 3308 estiver associada tooanother endereço e usa Olá o mesmo nome de usuário do MySQL e senha par somente Olá endereço de associação é necessária e hello outras propriedades serão herdadas.

Olá, a tabela a seguir tem as configurações de instância de exemplo 

| Descrição | Arquivo |
|:--|:--|
| Instância padrão e instância com porta 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Instância padrão e instância com porta 3308 e nome de usuário e senha diferentes. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Programa de Arquivo de Autenticação de OMI do MySQL
Provedor incluída com a instalação de saudação do hello OMI do MySQL é um programa de arquivo de autenticação de OMI do MySQL que pode ser um arquivo de autenticação de OMI do MySQL Olá tooedit usado. programa de arquivo Hello autenticação pode ser encontrado em Olá local a seguir.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> o arquivo de credenciais Olá deve ser legível por conta de omsagent hello. É recomendável executar o comando do hello mycimprovauth como omsgent.

Olá tabela a seguir fornece detalhes sobre a sintaxe de saudação para usando mycimprovauth.

| Operação | Exemplo | Descrição
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | Define se o arquivo de autenticação Olá será atualizado automaticamente na reinicie ou atualizar. |
| default *bind-address username password* | mycimprovauth default 127.0.0.1 root pwd | Conjuntos de hello a instância padrão no hello arquivo de autenticação de OMI do MySQL.<br>campo de senha Olá deve ser inserido em texto sem formatação - senha Olá Olá arquivo de autenticação de OMI do MySQL será codificada em Base 64. |
| delete *default\|port_num* | mycimprovauth 3308 | Exclui a instância especificada do hello por um padrão ou por número de porta. |
| ajuda | mycimprov help | Imprime uma lista de comandos toouse. |
| print | mycimprov print | Imprime um tooread fácil de arquivo de autenticação de OMI do MySQL. |
| update port_num *bind-address username password* | mycimprov update 3307 127.0.0.1 root pwd | Atualiza a instância especificada do hello ou adiciona instância Olá se ele não existe. |

Olá comandos de exemplo a seguir definem uma conta de usuário padrão para o MySQL server de saudação no localhost.  campo de senha Olá deve ser inserido em texto sem formatação - senha Olá Olá arquivo de autenticação de OMI do MySQL será codificada em Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Permissões de banco de dados necessárias para contadores de desempenho do MySQL
saudação de usuário do MySQL requer acesso toohello consultas toocollect dados de desempenho do MySQL Server a seguir. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


usuário do MySQL Olá também requer acesso SELECT toohello tabelas padrão a seguir.

- information_schema
- mysql. 

Esses privilégios podem ser concedidos, executando Olá comandos de concessão a seguir.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant permissões tooa saudação do usuário conceder usuário de monitoramento do MySQL deve ter Olá privilégio 'GRANT option', bem como privilégio Olá sendo concedido.

### <a name="define-performance-counters"></a>Definir contadores de desempenho

Depois que você configurar hello agente do OMS para Linux toosend dados tooLog análise, você deve configurar Olá toocollect de contadores de desempenho.  Use o procedimento Olá [fontes de dados de desempenho do Windows e Linux em análise de Log](log-analytics-data-sources-windows-events.md) com contadores Olá Olá a tabela a seguir.

| Nome do Objeto | Nome do contador |
|:--|:--|
| Banco de Dados MySQL | Espaço em Disco em Bytes |
| Banco de Dados MySQL | Tabelas |
| MySQL Server | % de Conexão Anulada |
| MySQL Server | % de Uso da Conexão |
| MySQL Server | Uso de Espaço em Disco em Bytes |
| MySQL Server | % da verificação de tabela completa |
| MySQL Server | % de Ocorrências no Pool de Buffers InnoDB |
| MySQL Server | % de Uso do Pool de Buffers InnoDB |
| MySQL Server | % de Uso do Pool de Buffers InnoDB |
| MySQL Server | % de Ocorrências no Cache de Chaves |
| MySQL Server | % de Uso do Cache de Chaves |
| MySQL Server | % de Gravação no Cache de Chaves |
| MySQL Server | % de Ocorrências no Cache de Consulta |
| MySQL Server | % de Remoções do Cache de Consulta |
| MySQL Server | % de Uso do Cache de Consulta |
| MySQL Server | % de Ocorrências no Cache de Tabela |
| MySQL Server | % de Uso do Cache de Tabela |
| MySQL Server | % de Contenção de Bloqueio de Tabela |

## <a name="apache-http-server"></a>Apache HTTP Server 
Se o Apache HTTP Server for detectado no computador de saudação quando o pacote do hello omsagent estiver instalado, um provedor para o Apache HTTP Server de monitoramento de desempenho será instalado automaticamente. Esse provedor baseia-se em um módulo Apache que deve ser carregado no hello Apache HTTP Server nos dados de desempenho de tooaccess de ordem. pode ser carregado módulo Olá Olá comando a seguir:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload Olá Apache módulo de monitoramento, execute Olá comando a seguir:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Definir contadores de desempenho

Depois que você configurar hello agente do OMS para Linux toosend dados tooLog análise, você deve configurar Olá toocollect de contadores de desempenho.  Use o procedimento Olá [fontes de dados de desempenho do Windows e Linux em análise de Log](log-analytics-data-sources-windows-events.md) com contadores Olá Olá a tabela a seguir.

| Nome do Objeto | Nome do contador |
|:--|:--|
| Apache HTTP Server | Trabalhos Ocupados |
| Apache HTTP Server | Trabalhos ociosos |
| Apache HTTP Server | % de Trabalhos Ocupados |
| Apache HTTP Server | % Total da CPU |
| Host Virtual Apache | Erros por Minuto – Cliente |
| Host Virtual Apache | Erros por Minuto – Servidor |
| Host Virtual Apache | KB por Solicitação |
| Host Virtual Apache | KB de Solicitações por Segundo |
| Host Virtual Apache | Solicitações por Segundo |



## <a name="next-steps"></a>Próximas etapas
* [Coletar contadores de desempenho](log-analytics-data-sources-performance-counters.md) de agentes do Linux.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções. 
