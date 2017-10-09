---
title: aaaSecuring bancos de dados de PaaS no Azure | Microsoft Docs
description: " Saiba mais sobre as melhores práticas de segurança do Banco de Dados SQL do Azure e do SQL Data Warehouse para proteger aplicativos Web e móveis PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Protegendo bancos de dados de PaaS no Azure

Neste artigo, discutiremos uma coleção de práticas recomendadas de segurança do [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) e do [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) para proteger seus aplicativos Web e móveis de PaaS. Essas práticas recomendadas são derivadas da nossa experiência com o Azure e experiências de saudação de clientes, como por conta própria.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Banco de Dados SQL do Azure e SQL Data Warehouse
O [Banco de Dados SQL do Azure](../sql-database/sql-database-technical-overview.md) e o [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) fornecem um serviço de banco de dados relacional para seus aplicativos baseados na Internet. Vamos examinar os serviços que ajudam a proteger seus aplicativos e dados ao usar o Banco de Dados SQL do Azure e o SQL Data Warehouse em uma implantação de PaaS:

- Autenticação do Azure Active Directory (em vez da autenticação do SQL Server)
- Firewall do SQL do Azure
- Transparent Data Encryption (TDE)

## <a name="best-practices"></a>Práticas recomendadas

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Usar um repositório de identidades centralizado para autenticação e autorização

Bancos de dados SQL do Azure podem ser configurado toouse um dos dois tipos de autenticação:

- A **Autenticação do SQL** usa um nome de usuário e senha. Quando você criou o servidor lógico Olá para seu banco de dados, você especificou um logon de "administrador do servidor" com um nome de usuário e senha. Usando essas credenciais, você pode autenticar tooany banco de dados no servidor como proprietário do banco de dados de saudação.

- A **Autenticação do Azure Active Directory** usa identidades gerenciadas pelo Azure Active Directory e que tem suporte para domínios gerenciados e integrados. toouse autenticação do Active Directory do Azure, você deve criar outro administrador de servidor chamado hello "Administrador do AD do Azure", que é permitido grupos e usuários do AD do Azure tooadminister. Este administrador também pode executar todas as operações executadas por um administrador de servidor comum.

[Autenticação do Active Directory do Azure](../active-directory/develop/active-directory-authentication-scenarios.md) é um mecanismo de conexão tooAzure banco de dados SQL e SQL Data Warehouse usando as identidades no Azure Active Directory (AD). AD do Azure fornece uma autenticação de servidor alternativo tooSQL, portanto você pode parar a proliferação de saudação de identidades de usuário entre os servidores de banco de dados. Habilita a autenticação AD do Azure toocentrally você gerenciar identidades de saudação de usuários de banco de dados e outros serviços da Microsoft em um local central. Central de gerenciamento de ID fornece um único local toomanage usuários de banco de dados e simplifica o gerenciamento de permissões.  

Os benefícios de usar a autenticação do Azure AD em vez da autenticação do SQL incluem:

- Permite o rodízio de senhas em um único lugar.
- Gerencia as permissões de banco de dados usando grupos externos do Azure AD.
- Elimina o armazenamento de senhas permitindo a autenticação integrada do Windows e outras formas de autenticação com suporte pelo Azure AD.
- Usa contidos identidades de tooauthenticate de usuários de banco de dados no nível de banco de dados de saudação.
- Oferece suporte à autenticação baseada em token para aplicativos que se conectam tooSQL banco de dados.
- Dá suporte ao ADFS (federação de domínio) ou à autenticação nativa de senha/usuário para um Azure AD local sem a sincronização de domínio.
- Dá suporte a conexões do SQL Server Management Studio que usam a Autenticação Universal do Active Directory, que inclui o [MFA (Autenticação Multifator)](../multi-factor-authentication/multi-factor-authentication.md). A MFA inclui autenticação eficiente com uma variedade de opções de verificação fáceis como chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis. Para saber mais, confira [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn mais sobre a autenticação do AD do Azure, consulte:

- [Conectando tooSQL banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md)
- [Autenticação tooAzure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Token-based authentication support for Azure SQL DB using Azure AD authentication](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/) (Suporte para autenticação baseada em token para o Banco de Dados SQL do Azure usando a autenticação do Azure AD)

> [!NOTE]
> tooensure Active Directory do Azure é uma boa opção para seu ambiente, consulte [recursos do AD do Azure e limitações](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), especificamente Olá considerações adicionais.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Restringir o acesso com base no endereço IP
Você pode criar regras de firewall que especifiquem intervalos de endereços IP aceitáveis. Essas regras podem ser afetadas nos níveis de banco de dados e de servidor de saudação. É recomendável usar as regras de firewall de nível de banco de dados sempre que possível tooenhance segurança e toomake seu banco de dados mais portáteis. Regras de firewall de nível de servidor são melhor usadas para administradores e quando você tem muitos bancos de dados que têm Olá mesmos requisitos de acesso, mas você não quiser tempo toospend configurar cada banco de dados individualmente.

As restrições de endereço IP de origem do Banco de Dados SQL permitem o acesso de qualquer endereço do Azure (incluindo outras assinaturas e locatários). Você pode restringir esse tooonly permitir sua instância de saudação do tooaccess de endereços IP. Mesmo com as restrições de endereço IP e firewall do SQL, a autenticação forte ainda é necessária. Consulte Olá recomendações feitas neste artigo.

toolearn mais sobre o Firewall do SQL Azure e restrições de IP, consulte:

- [Controle de acesso do Banco de Dados SQL do Azure](../sql-database/sql-database-control-access.md)
- [Configurar regras de firewall do Banco de Dados SQL do Azure – visão geral](../sql-database/sql-database-firewall-configure.md)
- [Configurar uma regra de firewall de nível de servidor de banco de dados SQL usando Olá portal do Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Criptografia de dados em repouso
A [TDE (Transparent Data Encryption)](https://msdn.microsoft.com/library/azure/bb934049) é habilitada por padrão. A TDE criptografa de forma transparente os arquivos de log e de dados do SQL Server, do Banco de Dados SQL do Azure e do SQL Data Warehouse do Azure. A TDE protege contra um comprometimento de seu backup ou arquivos de toohello acesso direto. Isso permite que você tooencrypt dados em repouso sem alterar os aplicativos existentes. TDE sempre deve permanecer habilitada; No entanto, isso não interromperá a um invasor que usa o caminho de acesso normal hello. TDE fornece Olá capacidade toocomply com muitas leis, regulamentos e diretrizes estabelecidas em vários setores.

O SQL do Azure gerencia problemas relacionados a chave para a TDE. Como com TDE, no local deve ter especial cuidado tooensure capacidade de recuperação e mover bancos de dados. Em cenários mais sofisticados, Olá chaves podem ser explicitamente gerenciadas no cofre de chaves do Azure por meio do gerenciamento extensível de chaves (consulte [habilitar TDE no SQL Server usando EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Isso também permite o BYOK (Bring Your Own Key) por meio da capacidade BYOK do Azure Key Vault.

O SQL do Azure fornece a criptografia para colunas por meio do [Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Isso permite o acesso de aplicativos autorizados somente toosensitive colunas. Usar esse tipo de criptografia limita consultas SQL para os valores com base em tooequality colunas criptografadas.

A criptografia do nível do aplicativo também deve ser usada para dados seletivos. Preocupações Soberania às vezes podem ser reduzidas com a criptografia de dados com uma chave que é mantida no país correto hello. Isso impede que o mesmo acidental de dados transferência causando um problema, já que é impossível toodecrypt Olá dados sem chave hello, supondo que um algoritmo forte são usados (por exemplo, AES 256).

Você pode usar o banco de dados do precauções adicionais toohelp Olá segura, como a criação de um sistema seguro, criptografando ativos confidenciais e criando um firewall em torno dos servidores de banco de dados de saudação.

## <a name="next-steps"></a>Próximas etapas
Este artigo introduzido você tooa coleção de banco de dados SQL e SQL Data Warehouse práticas recomendadas para proteger seu PaaS aplicativos web e móveis. toolearn mais sobre como proteger suas implantações de PaaS, consulte:

- [Proteção das implantações PaaS](security-paas-deployments.md)
- [Securing PaaS web and mobile applications using Azure App Services](security-paas-applications-using-app-services.md) (Proteção dos aplicativos Web e móveis de PaaS usando os Serviços de Aplicativos do Azure)
