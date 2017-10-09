---
title: "autenticação do Active Directory aaaAzure - SQL do Azure (visão geral) | Microsoft Docs"
description: "Saiba mais sobre como toouse Active Directory do Azure para autenticação com o banco de dados SQL e SQL Data Warehouse"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Usar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse
Autenticação do Active Directory do Azure é um mecanismo de conexão tooMicrosoft banco de dados do SQL Azure e [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) usando as identidades no Azure Active Directory (AD do Azure). Com a autenticação do AD do Azure, você pode gerenciar centralmente as identidades de saudação de usuários de banco de dados e outros serviços da Microsoft em um local central. Central de gerenciamento de ID fornece um único local toomanage usuários de banco de dados e simplifica o gerenciamento de permissões. Os benefícios incluem o seguinte hello:

* Ele fornece uma autenticação de servidor tooSQL alternativo.
* Ajuda a parar a proliferação de saudação de identidades de usuário entre os servidores de banco de dados.
* Permite o rodízio de senhas em um único lugar
* Os clientes podem gerenciar permissões de banco de dados usando grupos (AAD) externos.
* Pode eliminar o armazenamento de senhas, permitindo a autenticação integrada do Windows e outras formas de autenticação às quais o Active Directory do Azure dá suporte.
* Autenticação do Azure AD usa identidades de tooauthenticate de usuários de banco de dados independente em nível de banco de dados de saudação.
* O AD do Azure dá suporte à autenticação baseada em token para aplicativos que se conectam tooSQL banco de dados.
* A autenticação do Azure AD dá suporte ao ADFS (federação de domínio) ou à autenticação nativa de senha/usuário para um local do Azure Active Directory sem a sincronização de domínio.  
* O Azure AD dá suporte a conexões do SQL Server Management Studio que usam a Autenticação Universal do Active Directory, que inclui o MFA (Autenticação Multifator).  A MFA inclui autenticação eficiente com uma variedade de opções de verificação fáceis como chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis. Para saber mais, confira [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Conectando tooSQL Server em execução em uma VM do Azure não tem suporte com uma conta do Active Directory do Azure. Use um conta de domínio do Active Directory.  

etapas de configuração de saudação incluem hello tooconfigure procedimentos a seguir e usam a autenticação do Active Directory do Azure.

1. Criar e popular o Azure AD.
2. Opcional: Associar ou alterar Olá active directory que está associado a sua assinatura do Azure.
3. Crie um administrador do Azure Active Directory para o Azure SQL Server ou o [SQL Data Warehouse do Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Configure os computadores cliente.
5. Crie usuários de banco de dados independente em seu banco de dados mapeado tooAzure identidades do AD.
6. Conecte o banco de dados de tooyour usando identidades do AD do Azure.

> [!NOTE]
> toolearn como toocreate e preencher o AD do Azure e, em seguida, configurar o Azure AD com o banco de dados do SQL Azure e SQL Data Warehouse, consulte [configurar o AD do Azure com o Azure SQL Database](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Confiar na arquitetura
Olá diagrama de alto nível a seguir resume a arquitetura da solução de saudação do uso de autenticação do AD do Azure com o Azure SQL Database. Olá mesmos conceitos se aplicam tooSQL Data Warehouse. toosupport senha de usuário nativo de AD do Azure, apenas parte da nuvem hello e banco de dados SQL do Azure AD/é considerada. toosupport autenticação federada (ou usuário/senha para credenciais do Windows), é necessária a comunicação de saudação com bloco ADFS. setas de saudação indicam caminhos de comunicação.

![diagrama de autenticação do aad][1]

Olá diagrama a seguir indica federação hello, confiança e relações que permitem que um cliente de banco de dados de tooa tooconnect enviando um token de hospedagem. Olá token é autenticado pelo AD do Azure e é confiável pelo banco de dados de saudação. O Cliente 1 pode representar um Azure Active Directory com usuários nativos ou um Azure AD com usuários federados. O Cliente 2 representa uma solução possível, incluindo os usuários importados; neste exemplo, provenientes de um Azure Active Directory federado com o ADFS sendo sincronizado com o Azure Active Directory. É importante toounderstand que acessam o banco de dados tooa usando a autenticação do AD do Azure requer que Olá hospedagem assinatura é associada toohello AD do Azure. mesma assinatura Hello deve ser usado toocreate Olá do SQL Server hospedagem Olá banco de dados SQL ou SQL Data Warehouse.

![relação de assinatura][2]

## <a name="administrator-structure"></a>Estrutura do administrador
Ao usar a autenticação do AD do Azure, há duas contas de administrador do servidor de banco de dados SQL Olá; Olá administrador original do SQL Server e o administrador de saudação do AD do Azure. Olá mesmos conceitos se aplicam tooSQL Data Warehouse. Somente administrador Olá com base em uma conta do AD do Azure pode criar primeiro usuário de banco de dados do AD do Azure contido Olá em um banco de dados do usuário. logon de administrador do AD do Azure Olá pode ser um usuário do AD do Azure ou um grupo do AD do Azure. Administrador Olá é uma conta de grupo, ele pode ser usado por qualquer membro do grupo, permitindo que vários administradores do AD do Azure Olá instância do SQL Server. Toocentrally usando a conta de grupo como um administrador aprimora a capacidade de gerenciamento, permitindo que você adicionar e remover membros do grupo no AD do Azure sem alterar usuários hello ou permissões no banco de dados SQL. Somente um administrador do AD do Azure (um usuário ou grupo) pode ser configurado por vez, a qualquer momento.

![estrutura de administrador][3]

## <a name="permissions"></a>Permissões
toocreate novos usuários, você deve ter Olá `ALTER ANY USER` permissão no banco de dados de saudação. Olá `ALTER ANY USER` permissão pode ser concedida tooany usuário de banco de dados. Olá `ALTER ANY USER` permissão também é mantida por contas de administrador do servidor de saudação e usuários de banco de dados com hello `CONTROL ON DATABASE` ou `ALTER ON DATABASE` permissão do banco de dados e por membros da saudação `db_owner` função de banco de dados.

toocreate um usuário de banco de dados contido no banco de dados do SQL Azure ou o SQL Data Warehouse, você deve conectar o banco de dados de toohello usando uma identidade do AD do Azure. toocreate Olá primeiro banco de dados independente usuário, você deve conectar toohello banco de dados por meio de um administrador do AD do Azure (que é o proprietário de saudação do banco de dados de saudação). Isso é demonstrado nas etapas 4 e 5 abaixo. Qualquer autenticação do AD do Azure só é possível se Olá administrador do AD do Azure foi criado para o servidor de banco de dados do SQL Azure ou o SQL Data Warehouse. Se o administrador do Active Directory do Azure Olá foi removido do servidor de saudação, usuários existentes do Active Directory do Azure criados anteriormente no SQL Server não podem se conectar toohello banco de dados usando suas credenciais do Active Directory do Azure.

## <a name="azure-ad-features-and-limitations"></a>Limitações e recursos do AD do Azure
Olá membros do AD do Azure a seguir pode ser provisionada no SQL Azure server ou SQL Data Warehouse:

* Membros nativos: um membro criado no AD do Azure no domínio gerenciado hello ou em um domínio do cliente. Para obter mais informações, consulte [adicionar seu próprio nome de domínio tooAzure AD](../active-directory/active-directory-add-domain.md).
* Membros de domínio federado: membro criado no Azure AD com um domínio federado. Para saber mais, confira [O Microsoft Azure agora dá suporte à federação com o Active Directory do Windows Server](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Membros importados de outros Azure ADs que são membros de domínio nativo ou federado.
* Grupos do Active Directory criados como grupos de segurança.

Não há suporte para contas da Microsoft (por exemplo, outlook.com, hotmail.com, live.com) nem para outras contas de convidado (por exemplo, gmail.com, yahoo.com). Se você pode fazer logon muito[https://login.live.com](https://login.live.com) usando Olá conta e senha, e você estiver usando uma conta da Microsoft, que não há suporte para autenticação do AD do Azure para o banco de dados do SQL Azure ou Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Conectar-se usando as identidades do Azure AD

Autenticação do Active Directory do Azure dá suporte a saudação métodos do banco de dados de tooa conectar usando identidades do AD do Azure a seguir:

* Usando a autenticação integrada do Windows
* Uso de um nome principal e de uma senha do Azure AD
* Uso da autenticação de token do aplicativo

### <a name="additional-considerations"></a>Considerações adicionais

* tooenhance de capacidade de gerenciamento, é recomendável que você provisionar um AD do Azure dedicado grupo como um administrador.   
* Somente um administrador do Azure AD (um usuário ou grupo) pode ser configurado por vez, em qualquer determinado momento, para um Azure SQL Server ou SQL Data Warehouse do Azure.   
* Somente um administrador do AD do Azure para o SQL Server pode se conectar inicialmente toohello Azure SQL server ou do Azure SQL Data Warehouse usando uma conta do Active Directory do Azure. administrador do Active Directory Olá pode configurar subsequentes do AD do Azure usuários de banco de dados.   
* É recomendável definir segundos de too30 de tempo limite de conexão de saudação.   
* O SQL Server 2016 Management Studio e o SQL Server Data Tools para Visual Studio 2015 (versão 14.0.60311.1 de abril de 2016 ou posterior) dão suporte à autenticação do Azure Active Directory. (Olá dá suporte à autenticação do AD do azure **.NET Framework Data Provider para SQL Server**; pelo menos a versão do .NET Framework 4.6). Olá, portanto, as versões mais recentes dessas ferramentas e aplicativos da camada de dados (DAC e. bacpac) podem usar a autenticação do AD do Azure.   
* O [ODBC versão 13.1](https://www.microsoft.com/download/details.aspx?id=53339) dá suporte à autenticação do Azure Active Directory. No entanto, o `bcp.exe` não pode se conectar usando a autenticação do Azure Active Directory, pois usa um provedor ODBC mais antigo.   
* `sqlcmd`oferece suporte a partir do Active Directory do Azure autenticação versão 13.1 disponíveis da saudação [Centro de Download](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools para Visual Studio 2015 requer pelo menos versão de abril de 2016 de saudação do hello Data Tools (versão 14.0.60311.1). Atualmente, os usuários do Azure AD não são mostrados no Pesquisador de Objetos do SSDT. Como alternativa, exibir os usuários Olá [database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* O [Microsoft JDBC Driver 6.0 para SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) dá suporte à autenticação do Azure AD. Além disso, consulte [definindo propriedades de Conexão de saudação](https://msdn.microsoft.com/library/ms378988.aspx).   
* O PolyBase não pode ser autenticado com a autenticação do Azure AD.   
* Olá portal do Azure tem suporte para o banco de dados SQL do autenticação do Azure AD **importar banco de dados** e **Exportar banco de dados** folhas. Também há suporte para importação e exportação usando a autenticação do AD do Azure de saudação comando do PowerShell.   
* Há suporte para a autenticação do Azure AD no Banco de Dados SQL e SQL Data Warehouse usando a CLI. Para saber mais, veja [Configurar e gerenciar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse](sql-database-aad-authentication-configure.md) e [SQL Server – az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Próximas etapas
- toolearn como toocreate e preencher o AD do Azure e, em seguida, configurar o Azure AD com o banco de dados do SQL Azure ou Azure SQL Data Warehouse, consulte [configurar e gerenciar a autenticação do Active Directory do Azure com o banco de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Para obter uma visão geral de acesso e controle no Banco de Dados SQL, confira [Acesso e controle de Banco de Dados SQL](sql-database-control-access.md).
- Para obter uma visão geral de logons, usuários e funções de banco de dados no Banco de Dados SQL, confira [Logons, usuários e funções de banco de dados](sql-database-manage-logins.md).
- Para obter mais informações sobre objetos de banco de dados, confira [Entidades](https://msdn.microsoft.com/library/ms181127.aspx).
- Para obter mais informações sobre as funções de banco de dados, confira [Funções de banco de dados](https://msdn.microsoft.com/library/ms189121.aspx).
- Para obter mais informações sobre as regras de firewall no Banco de Dados SQL, confira [Regras de firewall de Banco de Dados SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

