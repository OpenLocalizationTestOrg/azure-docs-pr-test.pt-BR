---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Autenticação tooAzure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão Geral da Segurança](sql-data-warehouse-overview-manage-security.md)
> * [Autenticação](sql-data-warehouse-authentication.md)
> * [Criptografia (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Criptografia (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL Data Warehouse, você deve passar as credenciais de segurança para fins de autenticação. Após estabelecer uma conexão, determinadas configurações de conexão são definidas como parte do estabelecimento de sua sessão de consulta.  

Para obter mais informações sobre segurança e como tooenable conexões tooyour do data warehouse, consulte [proteger um banco de dados no Data Warehouse SQL][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Autenticação do SQL
tooconnect tooSQL Data Warehouse, você deve fornecer Olá informações a seguir:

* Nome totalmente qualificado do servidor
* Especificar a autenticação SQL
* Nome de Usuário
* Senha
* Banco de dados padrão (opcional)

Por padrão, sua conexão conecta toohello *mestre* banco de dados e não o banco de dados do usuário. dados de usuário de tooyour tooconnect, você pode escolher toodo uma das duas coisas:

* Especifique o banco de dados de padrão de saudação ao registrar seu servidor com hello Pesquisador de objetos do SQL Server no SSDT, SSMS, ou em sua cadeia de conexão do aplicativo. Por exemplo, inclua parâmetro InitialCatalog Olá uma conexão ODBC.
* Realce o banco de dados de usuário de saudação antes de criar uma sessão no SSDT.

> [!NOTE]
> Olá instrução Transact-SQL **USE MyDatabase;** não tem suporte para alterar o banco de dados de saudação para uma conexão. Para obter orientações sobre como conectar-se tooSQL Data Warehouse com o SSDT, consulte toohello [consulta com o Visual Studio] [ Query with Visual Studio] artigo.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Autenticação do AAD (Azure Active Directory)
[Active Directory do Azure] [ What is Azure Active Directory] autenticação é um mecanismo tooMicrosoft Azure SQL Data Warehouse para se conectar usando as identidades no Azure Active Directory (AD do Azure). Com a autenticação do Active Directory do Azure, você pode gerenciar centralmente as identidades de saudação de usuários de banco de dados e outros serviços da Microsoft em um local central. Central de gerenciamento de ID oferece um único local de usuários do SQL Data Warehouse toomanage e simplifica o gerenciamento de permissões. 

### <a name="benefits"></a>Benefícios
Os benefícios do Azure Active Directory incluem:

* Fornece uma autenticação de servidor tooSQL alternativo.
* Ajuda a parar a proliferação de saudação de identidades de usuário entre os servidores de banco de dados.
* Permite o rodízio de senhas em um único lugar
* Gerencia as permissões de banco de dados usando grupos externos (AAD).
* Elimina o armazenamento de senhas permitindo a autenticação integrada do Windows e outras formas de autenticação compatíveis com o Azure Active Directory.
* Usa contidos identidades de tooauthenticate de usuários de banco de dados no nível de banco de dados de saudação.
* Oferece suporte à autenticação baseada em token para aplicativos que se conectam tooSQL Data Warehouse.
* Dá suporte ao Multi-Factor Authentication por meio de Autenticação Universal do Active Directory para SQL Server Management Studio. Para obter uma descrição de Multi-Factor Authentication, consulte [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> O Azure Active Directory ainda é relativamente novo e tem algumas limitações. tooensure Active Directory do Azure é uma boa opção para seu ambiente, consulte [recursos do AD do Azure e limitações][Azure AD features and limitations], especificamente Olá considerações adicionais.
> 
> 

### <a name="configuration-steps"></a>Etapas da configuração
Execute a autenticação do Active Directory do Azure essas etapas tooconfigure.

1. Criar e popular um Azure Active Directory
2. Opcional: Associar ou alterar Olá active directory que está associado a sua assinatura do Azure
3. Criar um administrador do Azure Active Directory para o SQL Data Warehouse do Azure
4. Configurar os computadores cliente
5. Criar usuários de banco de dados independente em seu banco de dados mapeado tooAzure identidades do AD
6. Conectar-se a data warehouse de tooyour usando identidades do AD do Azure

Atualmente, os usuários do Azure Active Directory não são mostrados no Pesquisador de Objetos do SSDT. Como alternativa, exibir os usuários Olá [database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Localizar detalhes de saudação
* autenticação do Active Directory do Azure Olá etapas tooconfigure e uso são quase idênticas para o banco de dados do SQL Azure e o Azure SQL Data Warehouse. Siga Olá detalhadas etapas no tópico Olá [tooSQL conectando banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).
* Criar funções de banco de dados personalizados e adicionar usuários toohello funções. Em seguida, conceda permissões granulares toohello funções. Para obter mais informações, consulte o [Guia de introdução às Permissões do Mecanismo do Banco de Dados](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Próximas etapas
toostart consultando o data warehouse com o Visual Studio e outros aplicativos, consulte [consulta com o Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
