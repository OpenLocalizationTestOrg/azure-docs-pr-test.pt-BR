---
title: "autenticação de fator de aaaMulti - SQL do Azure | Microsoft Docs"
description: Use o Multi-Factor Authentication com SSMS para Banco de Dados SQL e SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Autenticação Universal com o Banco de Dados SQL e SQL Data Warehouse (suporte SSMS para MFA)
O Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure dão suporte a conexões do SSMS (SQL Server Management Studio) usando a *Autenticação Universal do Active Directory*. 
**Baixar Olá SSMS mais recentes** - no computador do cliente hello, baixe a versão mais recente de saudação do SSMS, de [baixar o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Todos os recursos de saudação neste tópico, use pelo menos julho de 2017, versão 17.2.  caixa de diálogo conexão mais recente Hello, tem esta aparência: ![1mfa-universal-conectar](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "caixa de nome de usuário Completes hello.")  

## <a name="hello-five-authentication-options"></a>Opções de autenticação Olá cinco  
- Autenticação do Active Directory Universal dá suporte a dois métodos de autenticação não interativo hello (`Active Directory - Password` autenticação e `Active Directory - Integrated` autenticação). Os métodos de Autenticação `Active Directory - Password` e `Active Directory - Integrated` não interativos podem ser usados em muitos aplicativos diferentes (ADO.NET, JDBC, ODBC, etc.). Esses dois métodos nunca resultam em caixas de diálogo pop-up.

- A autenticação `Active Directory - Universal with MFA` é um método interativo que também é compatível com a *Autenticação Multifator do Azure* (MFA). Azure MFA ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte com uma variedade de opções de verificação fácil (chamada telefônica, mensagem de texto, os cartões inteligentes com o pin ou a notificação de aplicativo móvel), permitindo que método de saudação do toochoose usuários que preferirem. O MFA interativo com o Azure AD pode resultar em uma caixa de diálogo pop-up para validação.

Para encontrar uma descrição do Multi-Factor Authentication, consulte [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Para etapas de configuração, consulte [Configurar Autenticação Multifator do Banco de Dados SQL do Azure para o SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Parâmetro de ID do locatário ou nome de domínio do Azure AD   

Começando com [SSMS versão 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), os usuários que são importados para Olá atual do Active Directory de outro Active Directories do Azure como usuários convidados, pode fornecer o nome de domínio de saudação do AD do Azure ou ID de locatário quando eles se conectam. Usuários convidados incluem usuários convidados de outros Azure ADs e contas Microsoft como outlook.com, hotmail.com, live.com ou outras contas como gmail.com. Essas informações permite **universais do Active Directory com a autenticação do MFA** tooidentify Olá correto de autoridade de autenticação. Essa opção também é necessário toosupport contas da Microsoft (MSA), como outlook.com, hotmail.com, live.com ou contas não MSA. Esses usuários que desejam toobe autenticado usando a autenticação Universal deve inserir seu nome de domínio do AD do Azure ou Locatário ID. Esse parâmetro representa Olá atual do AD do Azure domínio nome/locatário ID Olá com que servidor do Azure está vinculada. Por exemplo, se o servidor do Azure é associado ao domínio do AD do Azure `contosotest.onmicrosoft.com` onde usuário `joe@contosodev.onmicrosoft.com` hospedado como um usuário importado do domínio do AD do Azure `contosodev.onmicrosoft.com`, Olá tooauthenticate de necessário o nome de domínio, esse usuário é `contosotest.onmicrosoft.com`. Quando o usuário Olá é um usuário nativo de saudação do AD do Azure vinculado tooAzure Server e não é uma conta MSA, nenhuma ID de locatário ou de nome de domínio é necessário. tooenter Olá parâmetro (começando com o SSMS versão 17.2), Olá **conectar tooDatabase** caixa de diálogo, caixa de diálogo Olá completa, selecionando **do Active Directory - Universal com MFA** autenticação, Clique em **opções**, Olá completa **nome de usuário** caixa e, em seguida, clique em Olá **propriedades de Conexão** guia. Verificar Olá **ID de locatário ou de nome de domínio do AD** caixa e forneça a autoridade de autenticação, como nome de domínio da saudação (**contosotest.onmicrosoft.com**) ou Olá GUID da ID de locatário hello.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Suporte a toobusiness de negócios do Azure AD   
Os usuários do AD do Azure tem suportados para cenários de B2B do Azure AD como usuários convidados (consulte [novidades colaboração B2B do Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) pode se conectar tooSQL banco de dados e SQL Data Warehouse apenas como parte dos membros de um grupo criado no AD do Azure atual e mapeado manualmente usando Transact-SQL de Olá `CREATE USER` instrução em um determinado banco de dados. Por exemplo, se `steve@gmail.com` é tooAzure convidado AD `contosotest` (com o domínio do Ad do Azure Olá `contosotest.onmicrosoft.com`), grupo do AD do Azure, como `usergroup` devem ser criados no hello AD do Azure que contém Olá `steve@gmail.com` membro. Em seguida, esse grupo deve ser criado para um banco de dados específico (ou seja, MyDatabase) pelo administrador do SQL do Azure AD ou DBO do Azure AD executando uma instrução `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` do Transact-SQL. Após a criação de usuário de banco de dados hello, em seguida, Olá usuário `steve@gmail.com` pode fazer logon muito`MyDatabase` usando a opção de autenticação do SSMS Olá `Active Directory – Universal with MFA support`. Olá usergroup, por padrão, tem apenas Olá conectar-se qualquer acesso a dados adicional que precisará toobe concedido hello e permissão maneira normal. Observe que o usuário `steve@gmail.com` como um usuário convidado deve Olá caixa de seleção e adicionar o nome de domínio do AD de saudação `contosotest.onmicrosoft.com` em Olá SSMS **propriedade de Conexão** caixa de diálogo. Olá **ID de locatário ou de nome de domínio do AD** opção tem suporte apenas para Olá Universal com opções de conexão de MFA, caso contrário, ela está desativada.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limitações da Autenticação Universal para o Banco de Dados SQL e SQL Data Warehouse
* SSMS e SqlPackage.exe são ferramentas de somente Olá atualmente habilitadas para MFA por meio da autenticação Universal do Active Directory.
* O SSMS versão 17.2, dá suporte a acesso simultâneo de vários usuário usando a Autenticação Universal com MFA. Versão 17.0 e 17.1, restrito a um logon para uma instância do SSMS com autenticação Universal tooa única do Active Directory do Azure conta. toolog em que outra conta do AD do Azure, você deve usar outra instância do SSMS. (Essa restrição é limitada tooActive autenticação Universal do diretório; você pode fazer logon em servidores toodifferent usando a autenticação de senha do Active Directory, a autenticação integrada do Active Directory ou a autenticação do SQL Server).
* O SSMS dá suporte à Autenticação Universal do Active Directory para a visualização do Pesquisador de Objetos, do Editor de Consultas e do Repositório de Consultas.
* O SSMS versão 17.2 fornece suporte ao Assistente de DacFx para Eportação/Extração/Implantação de Dados de banco de dados. Quando um usuário específico é autenticado por meio do diálogo de autenticação inicial hello usando a autenticação Universal, hello funções DacFx Assistente Olá mesma maneira que faz para todos os outros métodos de autenticação.
* Olá Designer de tabela SSMS não dá suporte à autenticação Universal.
* Não há nenhum requisito de software adicional para a Autenticação Universal do Active Directory, exceto que você deve usar uma versão do SSMS com suporte.  
* versão da biblioteca de autenticação do Active Directory (ADAL) de saudação para autenticação Universal foi versão mais recente de ADAL.dll 3.13.9 disponível liberado tooits atualizado. Consulte [Biblioteca de Autenticação do Active Directory 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Próximas etapas

- Para etapas de configuração, consulte [Configurar Autenticação Multifator do Banco de Dados SQL do Azure para o SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Conceder a outros usuários acessar o banco de dados de tooyour: [autorização e autenticação do banco de dados SQL: concedendo acesso](sql-database-manage-logins.md)  
- Certifique-se de outros usuários podem se conectar por meio de firewall de saudação: [regra de firewall de configurar um nível de servidor de banco de dados SQL usando Olá portal do Azure](sql-database-configure-firewall-settings.md)  
- [Configurar e gerenciar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importar um tooa de arquivo BACPAC novo banco de dados do SQL do Azure](../sql-database/sql-database-import.md)  
- [Exportar um arquivo de BACPAC de tooa de banco de dados SQL do Azure](../sql-database/sql-database-export.md)  
- Interface C# [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
