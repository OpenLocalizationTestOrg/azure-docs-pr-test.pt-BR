---
title: "permissões de usuário e aaaAuthentication no Azure Analysis Services | Microsoft Docs"
description: "Saiba mais sobre as permissões de usuário e autenticação no Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Autenticação e permissões de usuário
O Azure Analysis Services usa o Azure AD (Azure Active Directory) para o gerenciamento de identidade e a autenticação de usuário. Qualquer usuário que está criando, gerenciando ou conectando tooan Azure Analysis Services server deve ter uma identidade de usuário válido uma [locatário do Azure AD](../active-directory/active-directory-administer.md) em Olá mesma assinatura.

O Azure Analysis Services dá suporte à [Colaboração B2B do Azure AD](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Com o B2B, os usuários de fora de uma organização podem ser convidados como usuários convidados em um diretório do Azure AD. Os convidados podem ser de outro diretório do locatário do Azure AD ou qualquer endereço de email válido. Convidou uma vez e usuário Olá aceita Olá convite enviado por email do Azure, hello identidade do usuário é adicionada toohello diretório do locatário. Essas identidades podem ser adicionadas a grupos de toosecurity ou como membros de uma função de banco de dados ou administrador do servidor.

![Arquitetura de autenticação do Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Autenticação
Todas as ferramentas e aplicativos cliente usam um ou mais de saudação do Analysis Services [bibliotecas de cliente](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa server. 

Todas as três bibliotecas de cliente dão suporte ao fluxo interativo do Azure AD e métodos de autenticação não interativos. Olá dois métodos não interativo, métodos de senha do Active Directory e a autenticação integrada do Active Directory podem ser usados em aplicativos utilizando AMOMD e MSOLAP. Esses dois métodos nunca resultam em caixas de diálogo pop-up.

Aplicativos cliente, como o Excel e Power BI Desktop, e ferramentas como o SSMS e SSDT instalam versões mais recentes de saudação das bibliotecas de saudação quando atualizado toohello última versão. O Power BI Desktop, o SSMS e o SSDT são atualizados mensalmente. O Excel é [atualizado com o Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Atualizações do Office 365 são menos frequentes e algumas organizações usam canal adiada hello, significado atualizações são adiadas backup toothree meses.

 Dependendo do aplicativo de cliente hello ou da ferramenta usada, o tipo de saudação de autenticação e como entrar pode ser diferente. Cada aplicativo pode dar suporte a recursos diferentes para se conectar a serviços toocloud como o Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Os servidores do Azure Analysis Services dão suporte a conexões do [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) e superior usando a Autenticação do Windows, a Autenticação de Senha do Active Directory e a Autenticação Universal do Active Directory. Em geral, é recomendável usar a Autenticação Universal do Active Directory porque:

*  Dá suporte a métodos de autenticação interativos e não interativos.

*  Oferece suporte a usuários convidados de B2B do Azure convidados em locatário do Azure como Olá. Ao conectar o servidor tooa, usuários convidados devem selecionar autenticação Universal do Active Directory ao conectar-se o servidor toohello.

*  Dá suporte à MFA (Autenticação Multifator). Azure MFA ajuda a proteger acesso toodata e aplicativos com uma variedade de opções de verificação: chamada telefônica, mensagem de texto, os cartões inteligentes com o pin ou a notificação de aplicativo móvel. O MFA interativo com o Azure AD pode resultar em uma caixa de diálogo pop-up para validação.

### <a name="sql-server-data-tools-ssdt"></a>SSDT (Ferramentas de Dados do SQL Server)
SSDT conecta tooAzure Analysis Services usando autenticação Universal do Active Directory com o suporte a MFA. Os usuários são solicitado toosign em tooAzure na primeira implantação de saudação usando sua ID organizacional (email). Os usuários devem entrar em tooAzure com uma conta com permissões de administrador de servidor no servidor de saudação está implantando. Ao entrar Olá tooAzure primeira vez, é atribuído um token. SSDT armazena em cache Olá token na memória para reconexão futuras.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop se conecta usando a autenticação Universal do Active Directory com o suporte a MFA do tooAzure Analysis Services. Os usuários são solicitado toosign em tooAzure na conexão primeiro hello usando sua ID organizacional (email). Os usuários devem entrar em tooAzure com uma conta que está incluída no administrador do servidor ou função de banco de dados.

### <a name="excel"></a>Excel
Os usuários do Excel podem se conectar a servidor tooa usando uma conta do Windows, uma ID de organização (endereço de email) ou um endereço de email externo. Identidades de email externo devem existir no hello AD do Azure como um usuário convidado.

## <a name="user-permissions"></a>Permissões de usuário

**Os administradores de servidor** são a instância do servidor de serviços de análise do Azure tooan específico. Eles se conectam com ferramentas como o portal do Azure, o SSMS e SSDT tooperform tarefas como adicionar bancos de dados e gerenciar funções de usuário. Por padrão, o usuário de saudação que cria o servidor de saudação automaticamente é adicionado como um administrador de servidor do Analysis Services. Outros administradores podem ser adicionados usando o SSMS ou o Portal do Azure. Os administradores de servidor devem ter uma conta no locatário de saudação do AD do Azure no hello mesma assinatura. mais, consulte toolearn [gerenciar administradores de servidor](analysis-services-server-admins.md). 


**Os usuários de banco de dados** se conectar a bancos de dados toomodel usando aplicativos cliente como Excel ou Power BI. Os usuários devem ser adicionados toodatabase funções. As funções de banco de dados definem a permissão de administrador, de leitura ou de processo para um banco de dados. É importante toounderstand usuários de banco de dados em uma função com permissões de administrador é diferente de administradores de servidor. No entanto, por padrão, os administradores de servidor também são administradores de banco de dados. mais, consulte toolearn [gerenciar usuários e funções de banco de dados](analysis-services-database-users.md).

**Proprietários de recursos do Azure**. Os proprietários do recurso gerenciam os recursos de uma assinatura do Azure. Os proprietários de recursos podem adicionar tooOwner de identidades de usuário do AD do Azure ou funções de Colaborador em uma assinatura usando **controle de acesso** no portal do Azure, ou com modelos do Gerenciador de recursos do Azure. 

![Controle de acesso no Portal do Azure](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Funções neste nível aplicam toousers ou contas que precisam de tooperform tarefas que podem ser concluídas no portal de saudação ou usando modelos do Gerenciador de recursos do Azure. mais, consulte toolearn [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Funções de banco de dados

 As funções definidas para um modelo tabular são funções de banco de dados. Ou seja, funções hello contêm membros que consistem em usuários do AD do Azure e os grupos de segurança que têm permissões específicas que definem a ação de saudação esses membros podem assumir um banco de dados de modelo. Uma função de banco de dados é criada como um objeto separado no banco de dados de saudação e aplica-se somente toohello banco de dados no qual a função foi criada.   
  
 Por padrão, quando você cria um novo projeto de modelo de tabela, projeto de modelo de saudação não tem nenhuma função. Funções podem ser definidas usando a caixa de diálogo Gerenciador de funções hello no SSDT. Quando as funções são definidas durante a criação do projeto de modelo, eles são aplicados toohello somente banco de dados de espaço de trabalho de modelo. Quando Olá modelo é implantado, hello mesmas funções são aplicadas toohello implantado modelo. Depois que um modelo foi implantado, os administradores de servidor e de banco de dados podem gerenciar funções e membros usando o SSMS. mais, consulte toolearn [gerenciar usuários e funções de banco de dados](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Próximas etapas

[Gerenciar acesso tooresources com grupos do Active Directory do Azure](../active-directory/active-directory-manage-groups.md)   
[Gerenciar usuários e funções de banco de dados](analysis-services-database-users.md)  
[Gerenciar administradores de servidor](analysis-services-server-admins.md)  
[Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md)  