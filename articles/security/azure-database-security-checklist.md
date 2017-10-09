---
title: "lista de verificação de segurança de banco de dados aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de lista de verificação de segurança do banco de dados do Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Lista de verificação de segurança do banco de dados do Azure

toohelp melhorar a segurança, o banco de dados do Azure inclui uma série de controles de segurança internas que você pode usar toolimit e controlar o acesso.

Estão incluídos:

-   Um firewall que permite que você toocreate [as regras de firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) limitando conectividade por endereço IP,
-   Firewall de nível de servidor acessível de saudação portal do Azure
-   Regras de firewall no nível de banco de dados acessíveis pelo SSMS
-   Banco de dados de tooyour de conectividade segura usando cadeias de caracteres de conexão segura
-   Usar gerenciamento de acesso
-   Criptografia de dados
-   Auditoria do Banco de Dados SQL
-   Detecção de ameaças do Banco de Dados SQL

## <a name="introduction"></a>Introdução
Exige novos paradigmas de segurança que são usuários do aplicativo toomany familiarizado, os administradores de banco de dados e programadores de computação em nuvem. Como resultado, algumas organizações são tooimplement hesitar uma infraestrutura de nuvem para o gerenciamento de dados devido a riscos de segurança tooperceived. No entanto, muito essa preocupação pode ser atenuado por meio de uma melhor compreensão dos recursos de segurança Olá incorporada ao Microsoft Azure e banco de dados SQL do Microsoft Azure.

## <a name="checklist"></a>Lista de verificação
É recomendável que você leia Olá [práticas recomendadas de segurança de banco de dados do Azure](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) artigo tooreviewing anterior esta lista de verificação. Você será capaz de tooget hello mais fora desta lista de verificação depois de entender as práticas recomendadas de saudação. Você pode usar este toomake de lista de verificação se você corrigiu problemas importantes Olá na segurança de banco de dados do Azure.


|Categoria da lista de verificação| Descrição|
| ------------ | -------- |
|**Proteger dados**||
| <br> Criptografia em movimento/trânsito| <ul><li>[Segurança de camada de transporte](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), criptografia de dados quando os dados se movem toohello redes.</li><li>Banco de dados requer uma comunicação segura de clientes com base em Olá [TDS (TDS)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protocolo sobre TLS (Transport Layer Security).</li></ul> |
|<br>Criptografia em repouso| <ul><li>[Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242), quando dados inativos são armazenados fisicamente em qualquer formato digital.</li></ul>|
|**Controlar acesso**||  
|<br> Acesso a banco de dados | <ul><li>[Autenticação](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Autenticação do Azure Active Directory), a autenticação do AD usa identidades gerenciadas pelo Azure Active Directory.</li><li>[Autorização](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) conceder a usuários Olá privilégios mínimos necessários.</li></ul> |
|<br>Acesso a aplicativos| <ul><li>[Segurança em nível de linha](https://msdn.microsoft.com/library/dn765131) (usando diretiva de segurança, Olá ao mesmo tempo, restringindo o acesso de nível de linha com base no contexto de execução, a função ou a identidade do usuário).</li><li>[Mascaramento de dados dinâmicos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (permissão usando & política, limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon)</li></ul>|
|**Monitoramento proativo**||  
| <br>Acompanhamento e detecção| <ul><li>[Auditoria](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) rastreia eventos de banco de dados e grava o log de auditoria tooan / atividade de log seu [conta de armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Acompanhe a integridade do banco de dados do Azure usando [Logs de atividades do Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Detecção de ameaças](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) detecta atividades anormais de banco de dados indicando potenciais database de toohello de ameaças de segurança. </li></ul> |
|<br>Central de Segurança do Azure| <ul><li>[Monitoramento de dados](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) Use a Central de Segurança do Azure como solução de monitoramento centralizado de segurança para SQL e outros serviços do Azure.</li></ul>|     

## <a name="conclusion"></a>Conclusão
O Banco de Dados do Azure é uma plataforma robusta de banco de dados, com uma gama completa de recursos de segurança que atendem aos vários requisitos de conformidade organizacional e regulamentar. Você pode proteger facilmente dados controlando os dados de tooyour saudação acesso físico e, em seguida, usando uma variedade de opções de segurança de dados no arquivo hello-, coluna ou nível de linha com a criptografia transparente de dados, a criptografia no nível da célula ou a segurança em nível de linha. Sempre criptografado também permite que as operações em relação aos dados criptografados, simplificando o processo de saudação de atualizações de aplicativo. Por sua vez, tooauditing acesso os logs de atividade de banco de dados SQL fornece informações de saudação for necessário, permitindo que você tooknow como e quando os dados são acessados.

## <a name="next-steps"></a>Próximas etapas
Você pode melhorar a proteção de saudação do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples. Neste tutorial, você aprenderá a:

- Configurar [regras de firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) para seu servidor e/ou banco de dados.
- Proteger seus dados com [criptografia](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Habilitar a [auditoria do Banco de Dados SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

