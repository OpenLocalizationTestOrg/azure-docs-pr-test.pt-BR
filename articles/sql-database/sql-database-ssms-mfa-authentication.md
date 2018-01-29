---
title: "Autenticação Multifator do Azure - SQL do Azure | Microsoft Docs"
description: "O Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure dão suporte a conexões do SSMS (SQL Server Management Studio) usando a Autenticação Universal do Active Directory."
services: sql-database
documentationcenter: 
author: GithubMirek
manager: johammer
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: On Demand
ms.date: 09/29/2017
ms.author: mireks
ms.openlocfilehash: 3fd6532fb3dc6af9b3ccdac37201552ad0475e7b
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2018
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Autenticação Universal com o Banco de Dados SQL e SQL Data Warehouse (suporte SSMS para MFA)
O Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure dão suporte a conexões do SSMS (SQL Server Management Studio) usando a *Autenticação Universal do Active Directory*. 
**Baixar a última versão do SSMS** - No computador cliente, baixe a última versão do SSMS em [Baixar o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Para todos os recursos neste tópico, use pelo menos a versão 17.2 de julho de 2017.  A caixa de diálogo de conexão mais recente, possui esta aparência: ![1mfa-universal-connect](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "Preenche a caixa de Nome de usuário.")  

## <a name="the-five-authentication-options"></a>As cinco opções de autenticação  
- A Autenticação Universal do Active Directory dá suporte a dois métodos de autenticação não interativa (autenticação `Active Directory - Password` e autenticação `Active Directory - Integrated`). Os métodos de Autenticação `Active Directory - Password` e `Active Directory - Integrated` não interativos podem ser usados em muitos aplicativos diferentes (ADO.NET, JDBC, ODBC, etc.). Esses dois métodos nunca resultam em caixas de diálogo pop-up.

- A autenticação `Active Directory - Universal with MFA` é um método interativo que também é compatível com a *Autenticação Multifator do Azure* (MFA). O Azure MFA ajuda a proteger o acesso a dados e aplicativos, ao mesmo tempo que atende à demanda dos usuários por um processo de entrada simples. Ele fornece autenticação eficiente com uma variedade de opções de verificação fáceis, como chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis, os quais permitem que os usuários escolham seu método de preferência. O MFA interativo com o Azure AD pode resultar em uma caixa de diálogo pop-up para validação.

Para encontrar uma descrição da Autenticação Multifator, consulte [Autenticação Multifator](../multi-factor-authentication/multi-factor-authentication.md).
Para etapas de configuração, consulte [Configurar Autenticação Multifator do Banco de Dados SQL do Azure para o SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Parâmetro de ID do locatário ou nome de domínio do Azure AD   

Começando com o [SSMS versão 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), os usuários que são importados para o Active Directory atual de outros Azure Active Directories como usuários convidados, podem fornecer a ID de locatário ou nome de domínio do Azure AD quando eles se conectam. Usuários convidados incluem usuários convidados de outros Azure ADs e contas Microsoft como outlook.com, hotmail.com, live.com ou outras contas como gmail.com. Essa informação, permite que o **Active Directory Universal com Autenticação MFA** identifique a autoridade de autenticação correta. Essa opção também é necessária para dar suporte a contas da Microsoft (MSA), como outlook.com, hotmail.com, live.com ou contas que não são MSA. Todos esses usuários que desejam ser autenticados usando a autenticação Universal devem inserir sua ID de locatário ou nome de domínio do Azure AD. Esse parâmetro representa a ID de locatário/nome de domínio do Azure AD atual a que o Servidor do Azure está vinculado. Por exemplo, se o servidor do Azure está associado com o domínio do Azure AD `contosotest.onmicrosoft.com` em que o usuário `joe@contosodev.onmicrosoft.com` está hospedado como um usuário importado do domínio do Azure AD `contosodev.onmicrosoft.com`, o nome de domínio necessário para autenticar esse usuário é `contosotest.onmicrosoft.com`. Quando o usuário é um usuário nativo do Azure AD vinculado ao Servidor do Azure e não é uma conta MSA, nenhuma ID de locatário nem nome de domínio é necessário. Para inserir o parâmetro (começando com o SSMS versão 17.2), na caixa de diálogo **Conectar-se ao banco de dados**, preencha a caixa de diálogo, selecionando a autenticação **Active Directory - Universal com MFA**, clique em **Opções**, preencha a caixa de **Nome de usuário** e, em seguida, clique na guia **Propriedades de conexão**. Marque a caixa **ID de locatário ou nome de domínio do AD** e forneça a autoridade de autenticação, como o nome de domínio (**contosotest.onmicrosoft.com**) ou o GUID da ID do locatário.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-to-business-support"></a>Suporte entre empresas do Azure AD   
Os usuários do Azure AD com suporte para cenários de B2B do Azure AD como usuários convidados (consulte [O que é colaboração B2B do Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) podem se conectar ao Banco de Dados SQL e SQL Data Warehouse apenas como parte dos membros de um grupo criado no Azure AD atual e mapeados manualmente usando a instrução `CREATE USER` do Transact-SQL em um determinado banco de dados. Por exemplo, se `steve@gmail.com` é convidado para o Azure AD `contosotest` (com o domínio do Azure Ad `contosotest.onmicrosoft.com`), um grupo do Azure AD, como `usergroup` deve ser criado no Azure AD que contém o membro `steve@gmail.com`. Em seguida, esse grupo deve ser criado para um banco de dados específico (ou seja, MyDatabase) pelo administrador do SQL do Azure AD ou DBO do Azure AD executando uma instrução `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` do Transact-SQL. Depois que o usuário de banco de dados for criado o usuário `steve@gmail.com` pode fazer logon em `MyDatabase` usando a opção `Active Directory – Universal with MFA support` de autenticação do SSMS. O grupo de usuários, por padrão, possui somente a permissão de conexão e qualquer acesso a dados adicional precisará ser concedido da maneira normal. Observe que o usuário `steve@gmail.com` como um usuário convidado deve marcar a caixa e adicionar o nome de domínio do AD `contosotest.onmicrosoft.com` na caixa de diálogo **Propriedade de Conexão** do SSMS. A opção **ID de locatário ou nome de domínio do AD** tem suporte apenas para opções de conexão Universal com MFA, caso contrário, ela fica acinzentada.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limitações da Autenticação Universal para o Banco de Dados SQL e SQL Data Warehouse
- O SSMS e o SqlPackage.exe são as únicas ferramentas atualmente habilitadas para MFA por meio da Autenticação Universal do Active Directory.
- O SSMS versão 17.2, dá suporte a acesso simultâneo de vários usuário usando a Autenticação Universal com MFA. As versões 17.0 e 17.1 restringiam o logon para uma instância do SSMS usando Autenticação Universal a uma única conta do Azure Active Directory. Para fazer logon como outra conta do Azure AD, você deve usar outra instância do SSMS. (Essa restrição é limitada à Autenticação Universal do Active Directory, você pode fazer logon em diferentes servidores usando a Autenticação de Senha do Active Directory, a Autenticação Integrada do Active Directory ou a Autenticação do SQL Server).
- O SSMS dá suporte à Autenticação Universal do Active Directory para a visualização do Pesquisador de Objetos, do Editor de Consultas e do Repositório de Consultas.
- O SSMS versão 17.2 fornece suporte ao Assistente de DacFx para Eportação/Extração/Implantação de Dados de banco de dados. Depois que um usuário específico é autenticado por meio da caixa de diálogo de autenticação inicial usando a Autenticação Universal, o Assistente de DacFx funciona da mesma maneira que faz para todos os outros métodos de autenticação.
- O Designer de Tabela de SSMS não dá suporte à Autenticação Universal.
- Não há nenhum requisito de software adicional para a Autenticação Universal do Active Directory, exceto que você deve usar uma versão do SSMS com suporte.  
- A versão da Biblioteca de Autenticação do Active Directory (ADAL) para autenticação Universal foi atualizada para a última versão lançada disponível de ADAL.dll 3.13.9. Consulte [Biblioteca de Autenticação do Active Directory 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).  


## <a name="next-steps"></a>Próximas etapas

- Para etapas de configuração, consulte [Configurar Autenticação Multifator do Banco de Dados SQL do Azure para o SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Conceder acesso a outros a seu banco de dados: [Autenticação e Autorização do Banco de Dados SQL: Concessão de Acesso](sql-database-manage-logins.md)  
- Verifique se os outros podem se conectar pelo firewall: [Configurar uma regra de firewall no nível de servidor do Banco de Dados SQL do Azure usando o Portal do Azure](sql-database-configure-firewall-settings.md)  
- [Configurar e gerenciar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importar um arquivo BACPAC para um novo Banco de Dados SQL do Azure](../sql-database/sql-database-import.md)  
- [Exportar um Banco de Dados SQL do Azure para um arquivo BACPAC](../sql-database/sql-database-export.md)  
- Interface C# [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
- Ao usar a autenticação **Active Directory - Universal com MFA**, o rastreamento ADAL está disponível a partir do [SSMS 17.3](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Desativado por padrão, você pode ativar o rastreamento ADAL usando o menu **Ferramentas**, no menu **Opções**, em **Serviços do Azure**, **Nuvem do Azure**, **Nível de rastreamento de janela de saída ADAL** e, em seguida, habilitando **Saída** no menu **Exibição**. Os rastreamentos estão disponíveis na janela de saída ao selecionar a **opção do Active Directory do Azure**.  
