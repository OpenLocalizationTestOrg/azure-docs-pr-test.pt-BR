---
title: "a autenticação multifator aaaConfigure - SQL do Azure | Microsoft Docs"
description: Use o Multi-Factor Authentication com SSMS para Banco de Dados SQL e SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Configurar a autenticação multifator para SQL Server Management Studio e Azure AD

Este tópico mostra como autenticação multifator do Azure Active Directory toouse (MFA) com o SQL Server Management Studio. MFA do Azure AD pode ser usado ao conectar-se o SSMS ou SqlPackage.exe tooAzure banco de dados SQL e o Azure SQL Data Warehouse.

Para obter uma visão geral da autenticação multifator do Banco de Dados SQL do Azure, consulte [Autenticação Universal com o Banco de Dados SQL e o SQL Data Warehouse (suporte do SSMS para MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Etapas da configuração

1. **Configurar um Active Directory do Azure** - para obter mais informações, consulte [administrando seu diretório do AD do Azure](https://msdn.microsoft.com/library/azure/hh967611.aspx), [integrando suas identidades locais ao Active Directory do Azure](../active-directory/active-directory-aadconnect.md), [Adicionar seu próprio nome de domínio tooAzure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure agora oferece suporte à Federação com o Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), e [gerenciar o AD do Azure usando o Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Configurar o MFA** – para obter instruções passo a passo, veja [O que é a Autenticação Multifator do Azure?](../multi-factor-authentication/multi-factor-authentication.md), [Acesso Condicional (MFA) com o Banco de Dados SQL do Azure e o Data Warehouse](sql-database-conditional-access.md). (O acesso condicional completo exige um Azure Active Directory (Azure AD) Premium. MFA limitado está disponível com um Azure AD padrão).
3. **Configurar o banco de dados SQL ou SQL Data Warehouse para autenticação do Azure AD** - para obter instruções passo a passo, consulte [tooSQL conectando banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](sql-database-aad-authentication.md).
4. **Baixar o SSMS** - no computador do cliente hello, baixar Olá SSMS mais recentes, de [baixar o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Todos os recursos de saudação neste tópico, use pelo menos julho de 2017, versão 17.2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Conectando-se usando a autenticação universal com o SSMS

Olá, as etapas a seguir mostra como tooconnect tooSQL banco de dados ou o SQL Data Warehouse usando Olá SSMS mais recentes.

1. tooconnect usando a autenticação Universal, em Olá **conectar tooServer** caixa de diálogo, selecione **do Active Directory - Universal com suporte do MFA**. (Se você vir **autenticação Universal do Active Directory** não estão na versão mais recente de saudação do SSMS.)  
   ![1mfa-universal-connect][1]  
2. Olá completa **nome de usuário** caixa com credenciais do Active Directory do Azure hello, no formato de saudação `user_name@domain.com`.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Se você estiver se conectando como um usuário convidado, você deve clicar em **opções**e em Olá **propriedade de Conexão** caixa de diálogo, Olá completa **ID de locatário ou de nome de domínio do AD** caixa. Para saber mais, veja [Autenticação Universal com o Banco de Dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](sql-database-ssms-mfa-authentication.md).
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. Como de costume de banco de dados SQL e SQL Data Warehouse, você deve clicar em **opções** e especifique o banco de dados Olá Olá **opções** caixa de diálogo. (Se Olá conectado é um usuário convidado (ou seja, joe@outlook.com), você deve Olá caixa de seleção e adicionar ID de nome ou Locatário do domínio Olá AD atual como parte das opções. Veja [Autenticação Universal com o Banco de Dados SQL e o SQL Data Warehouse (suporte do SSMS para MFA)]()(sql-database-ssms-mfa-authentication.md. E clique em **Conectar**.  
5. Olá quando **entrar na conta tooyour** caixa de diálogo for exibida, forneça Olá conta e uma senha de sua identidade do Active Directory do Azure. Nenhuma senha será necessária se um usuário fizer parte de um domínio federado com o Azure AD.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > Para a Autenticação Universal com uma conta que não exige o MFA, você se conecta neste momento. Para usuários exigir MFA, continue com hello etapas a seguir:
   >  
   
6. Devem aparecer duas caixas de diálogo de configuração de MFA. Dessa vez operação depende do administrador do MFA Olá configuração e, portanto, pode ser opcional. Esta etapa às vezes é predefinida para um domínio MFA habilitado (por exemplo, domínio Olá requer usuários toouse um cartão inteligente e pin).  
   ![3mfa-setup][3]  
7. Olá possível segunda caixa de diálogo permite que você tooselect detalhes de saudação do seu método de autenticação de uma vez. opções possíveis Olá são configuradas pelo administrador.  
   ![4mfa-verify-1][4]  
8. Olá Active Directory do Azure envia Olá confirmando tooyou de informações. Quando você receber o código de verificação de hello, inseri-la na Olá **insira o código de verificação** caixa e clique em **entrar**.  
   ![5mfa-verify-2][5]  

Quando a verificação for concluída, o SSMS se conectará normalmente considerando as credenciais válidas e o acesso ao firewall.

## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral da autenticação multifator do Banco de Dados SQL do Azure, consulte [Autenticação Universal com o Banco de Dados SQL e o SQL Data Warehouse (suporte do SSMS para MFA)](sql-database-ssms-mfa-authentication.md).
* Conceder a outros usuários acessar o banco de dados de tooyour: [autorização e autenticação do banco de dados SQL: concedendo acesso](sql-database-manage-logins.md)  
Certifique-se de outros usuários podem se conectar por meio de firewall de saudação: [regra de firewall de configurar um nível de servidor de banco de dados SQL usando Olá portal do Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

