---
title: "Visão geral de segurança de banco de dados SQL do aaaAzure | Microsoft Docs"
description: "Saiba mais sobre a segurança de banco de dados do SQL Azure e SQL Server, incluindo diferenças de saudação entre a nuvem de saudação e o local do SQL Server quando se trata de tooauthentication, autorização, segurança de conexão, criptografia e conformidade."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Protegendo o Banco de Dados SQL

Este artigo explica os fundamentos de Olá de proteção da camada de dados de saudação de um aplicativo usando o banco de dados do SQL Azure. Em particular, este artigo mostrará uma introdução aos recursos de proteção de dados, de controle de acesso e de monitoramento proativo. 

Para obter uma visão geral completa dos recursos de segurança disponíveis em todas as versões do SQL, consulte Olá [Central de segurança do mecanismo de banco de dados do SQL Server e banco de dados do SQL Azure](https://msdn.microsoft.com/library/bb510589). Informações adicionais também estão disponíveis no hello [segurança e o banco de dados do SQL Azure white paper técnico](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Proteger dados
O Banco de Dados SQL protege dados, fornecendo criptografia de dados em movimento usando o [protocolo TLS](https://support.microsoft.com/kb/3135244), para dados em repouso usando [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) e para dados em uso usando [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Todas as conexões tooAzure banco de dados SQL exigir criptografia SSL/TLS () em todas as vezes enquanto os dados são tooand "em trânsito" do banco de dados de saudação. Na cadeia de caracteres de conexão do seu aplicativo, você deve especificar a conexão de saudação do parâmetros tooencrypt e *não* tootrust Olá certificado do servidor (Isso é feito para você se você copiar a cadeia de caracteres de conexão de Olá Portal clássico do Azure) Caso contrário, conexão Olá não irá verificar a identidade de saudação do servidor de saudação e estará suscetíveis ataques de muito "man-in-the-middle". Para o driver do ADO.NET hello, por exemplo, esses parâmetros de cadeia de caracteres de conexão são **Encrypt = True** e **TrustServerCertificate = False**. 

Para outra maneiras tooencrypt seus dados, considere:

* [Criptografia em nível de célula](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colunas específicas ou mesmo células de dados com diferentes chaves de criptografia.
* Se você precisar de um Módulo de Segurança de Hardware ou do gerenciamento central de sua hierarquia de chaves de criptografia, considere o uso do [cofre da chave do Azure com o SQL Server em uma VM do Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Controlar o acesso
Banco de dados SQL protege seus dados por meio da limitação tooyour banco de dados usando regras de firewall, exigindo usuários tooprove sua identidade e autorização toodata por meio de permissões e associações de função, bem como por meio de mecanismos de autenticação segurança em nível de linha e mascaramento de dados dinâmicos. Para uma discussão sobre o uso de saudação de recursos de controle de acesso no banco de dados SQL, consulte [controlar o acesso](sql-database-control-access.md).

> [!IMPORTANT]
> O gerenciamento de bancos de dados e de servidores lógicos no Azure é controlado por atribuições de função da sua conta de usuário do portal. Para saber mais sobre esse tópico, confira [Controle de acesso baseado em função no portal do Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Firewall e regras de firewall
toohelp proteger seus dados, firewalls impedem todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão usando [as regras de firewall](sql-database-firewall-configure.md). firewall de saudação concede acesso toodatabases com base em Olá endereços IP de cada solicitação de origem.

### <a name="authentication"></a>Autenticação
Autenticação do banco de dados SQL refere-se toohow provar sua identidade ao conectar-se o banco de dados toohello. O Banco de Dados SQL dá suporte a dois tipos de autenticação:

* **Autenticação do SQL**, que usa um nome de usuário e senha. Quando você criou o servidor lógico Olá para seu banco de dados, você especificou um logon de "administrador do servidor" com um nome de usuário e senha. Usando essas credenciais, você pode autenticar tooany banco de dados no servidor como proprietário do banco de dados hello, ou "dbo". 
* **Autenticação do Azure Active Directory**, que usa identidades gerenciadas pelo Azure Active Directory e que tem suporte para domínios gerenciados e integrados. Use autenticação do Active Directory (segurança integrada) [sempre que possível](https://msdn.microsoft.com/library/ms144284.aspx). Se você quiser toouse autenticação do Active Directory do Azure, você deve criar outro administrador de servidor chamado hello "Administrador do AD do Azure", que é permitido grupos e usuários do AD do Azure tooadminister. Este administrador também pode executar todas as operações executadas por um administrador de servidor comum. Consulte [conexão tooSQL banco de dados, usando o Azure Active Directory Authentication](sql-database-aad-authentication.md) para obter uma explicação de como toocreate uma tooenable de administração do AD do Azure autenticação do Active Directory do Azure.

### <a name="authorization"></a>Autorização
Autorização refere-se toowhat um usuário pode fazer em um banco de dados do SQL Azure, e isso é controlado por associações de função de banco de dados da sua conta de usuário e nível de objeto permissões. Como prática recomendada, você deve conceder Olá usuários privilégios mínimos necessários. conta de administrador de servidor Olá que você está se conectando é membro de db_owner, que tem autoridade toodo nada no banco de dados de saudação. Salve essa conta para implantar atualizações de esquema e outras operações de gerenciamento. Usar conta de "ApplicationUser" hello com tooconnect mais limitado de permissões de banco de dados de toohello seu aplicativo com hello privilégios mínimos necessitados para seu aplicativo.

### <a name="row-level-security"></a>Segurança em nível de linha
Segurança em nível de linha permite que os clientes toocontrol acesso toorows em uma tabela de banco de dados com base em características de saudação do usuário Olá executando uma consulta (por exemplo, grupo associação ou contexto de execução). Para saber mais, confira [Segurança em nível de linha](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Mascaramento de dados 
Mascaramento de dados dinâmicos do banco de dados SQL limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon. Dados dinâmicos mascaramento automaticamente descobre dados potencialmente confidenciais no banco de dados do SQL Azure e fornece recomendações viáveis toomask esses campos, com impacto mínimo sobre a camada de aplicativo hello. Ele funciona por Ofuscando dados confidenciais saudação no conjunto de resultados de saudação de uma consulta em relação aos campos do banco de dados designados, enquanto dados Olá no banco de dados de saudação não são alterados. Para obter mais informações, consulte [Introdução ao mascaramento de dados dinâmicos do banco de dados SQL](sql-database-dynamic-data-masking-get-started.md) pode ser usado toolimit exposição de dados confidenciais.

## <a name="proactive-monitoring"></a>Monitoramento proativo
O Banco de Dados SQL protege seus dados, fornecendo a auditoria e recursos de detecção de ameaças. 

### <a name="auditing"></a>Auditoria
Auditoria de banco de dados SQL rastreia atividades de banco de dados e ajuda a conformidade com as normas toomaintain, registrando em log de auditoria do banco de dados eventos tooan em sua conta de armazenamento do Azure. Auditoria permite que você toounderstand atividades de banco de dados em andamento, bem como analisar e investigue potenciais ameaças de tooidentify de atividade de histórico ou suspeitas de violações de segurança e abuso. Para saber mais, confira [Introdução à Auditoria do Banco de Dados SQL](sql-database-auditing.md).  

### <a name="threat-detection"></a>Detecção de ameaças
A detecção de ameaças complementa a auditoria, fornecendo uma camada adicional de inteligência de segurança incorporada ao serviço de banco de dados do Azure SQL Olá que detecta tentativas incomuns e potencialmente prejudiciais tooaccess ou exploração bancos de dados. Você será alertado sobre atividades suspeitas, vulnerabilidades potenciais, ataques de injeção de SQL, bem como padrões de acesso do banco de dados anormais. Alertas de detecção de ameaças que podem ser exibidas no [Central de segurança do Azure](https://azure.microsoft.com/services/security-center/) e fornecer detalhes de atividade suspeita e recomendarão a ação sobre como tooinvestigate e atenuar a ameaça de saudação. A Detecção de Ameaças custa US$ 15/servidor/mês. É gratuito para Olá primeiros 60 dias. Para obter mais informações, confira [Introdução à Detecção de Ameaças do Banco de Dados SQL](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Mascaramento de dados 
Mascaramento de dados dinâmicos do banco de dados SQL limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon. Dados dinâmicos mascaramento automaticamente descobre dados potencialmente confidenciais no banco de dados do SQL Azure e fornece recomendações viáveis toomask esses campos, com impacto mínimo sobre a camada de aplicativo hello. Ele funciona por Ofuscando dados confidenciais saudação no conjunto de resultados de saudação de uma consulta em relação aos campos do banco de dados designados, enquanto dados Olá no banco de dados de saudação não são alterados. Para saber mais, confira a Introdução ao [mascaramento de dados dinâmicos do Banco de Dados SQL](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Conformidade
Além disso, toohello acima recursos e funcionalidades que podem ajudar seu aplicativo a atender a vários requisitos de segurança, o banco de dados do SQL Azure também participa de auditorias regulares e foi certificado em um número de padrões de conformidade. Para obter mais informações, consulte Olá [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), onde você pode encontrar a lista atualizada de saudação do [certificações de conformidade do banco de dados SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Próximas etapas

- Para uma discussão sobre o uso de saudação de recursos de controle de acesso no banco de dados SQL, consulte [controlar o acesso](sql-database-control-access.md).
- Para uma discussão sobre auditoria de banco de dados, consulte [Auditoria de Banco de Dados SQL](sql-database-auditing.md).
- Para uma discussão sobre detecção de ameaças, consulte [Detecção de ameaças do Banco de Dados SQL](sql-database-threat-detection.md).
