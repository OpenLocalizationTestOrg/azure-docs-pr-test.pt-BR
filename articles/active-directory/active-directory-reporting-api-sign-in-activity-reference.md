---
title: "relatório de atividade aaaAzure sign-in do Active Directory referência de API | Microsoft Docs"
description: "Referência para o relatório de atividade de saudação do Active Directory do Azure entrar API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Referência da API de relatório de atividade de entrada do Azure Active Directory
Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.  
Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de relatório de atividade de entrada usando o código ou ferramentas relacionadas.
escopo de saudação deste tópico é tooprovide você com informações de referência sobre Olá **API de relatório de atividade de entrada**.

Consulte:

* [Atividades de entrada](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais
* [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.


## <a name="who-can-access-hello-api-data"></a>Quem pode acessar dados de API Olá?
* Os usuários e entidades de serviço na função de administrador de segurança ou segurança leitor Olá
* Administradores globais
* Qualquer aplicativo que tenha autorização tooaccess Olá API (o autorização de aplicativo pode ser configurado somente com base na permissão do Administrador Global)

acesso de tooconfigure para um aplicativo tooaccess segurança APIs como eventos de entrada, Olá use aplicativos de saudação do PowerShell tooadd entidade de serviço a seguir à função de leitor de segurança Olá

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Pré-requisitos
Esse relatório por meio de tooaccess Olá API de relatório, você deve ter:

* Um [Azure Active Directory Premium edição P1 ou P2](active-directory-editions.md)
* Olá concluído [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Acessando a API de saudação
É possível acessar essa API por meio de saudação [Gerenciador de gráficos](https://graphexplorer2.cloudapp.net) ou programaticamente, usando, por exemplo, do PowerShell. Para toocorrectly PowerShell interpretar a sintaxe de filtro OData Olá usada nas chamadas AAD Graph REST, você deve usar Olá acento (também conhecido como: acento grave) caractere muito "caractere de escape" hello $. caractere de acento grave Olá serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell toodo uma interpretação de literal de caractere de $ hello e evitar confundi-lo como um nome de variável do PowerShell (ou seja: $filter).

Olá foco deste tópico é Olá Gerenciador de gráficos. Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Ponto de extremidade de API
Você pode acessar essa API usando Olá URI de base a seguir:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Devido a toohello o volume de dados, essa API tem um limite de um milhão de registros retornados. 

Essa chamada retorna dados saudação em lotes. Cada lote tem no máximo 1000 registros.  
tooget Olá próximo lote de registros, use Olá próximo link. Obter Olá [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informações do primeiro conjunto de registros retornados de saudação. símbolo de salto Olá será final Olá Olá do conjunto de resultados.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtros com suporte
Você pode reduzir o número de saudação de registros que são retornados por uma API chamada na forma de um filtro.  
Para entrar API dados relacionados, Olá filtros a seguir têm suporte:

* **$top =\<retornado do número de registros toobe\>**  -número de saudação toolimit de registros retornados. Esta é uma operação cara. Você não deve usar esse filtro se quiser tooreturn milhares de objetos.  
* **$filter =\<sua instrução de filtro\>**  -toospecify, cada saudação de campos de filtro com suporte, tipo de saudação de registros que importam

## <a name="supported-filter-fields-and-operators"></a>Campos de filtro e operadores com suporte
tipo de saudação toospecify de registros importantes para você, você pode criar uma instrução de filtro que pode conter um ou uma combinação de saudação campos de filtro a seguir:

* [signinDateTime](#signindatetime) – Define uma data ou intervalo de datas
* [userId](#userid) -define a ID. do usuário de saudação um usuário específico com base
* [userPrincipalName](#userprincipalname) -define o nome principal do usuário de saudação um usuário específico com base em usuário (UPN)
* [appId](#appid) -define a ID do aplicativo hello um aplicativo específico com base em
* [appDisplayName](#appdisplayname) -define o nome para exibição do aplicativo hello um aplicativo específico com base em
* [status de logon](#loginStatus) -define o status de saudação de logons de saudação (êxito / falha)

> [!NOTE]
> Ao usar o Gerenciador de gráficos, você Olá necessário toouse Olá correto para cada letra é seus campos de filtro.
> 
> 

toonarrow escopo de saudação da saudação retornada dados, você pode criar combinações de filtros de saudação com suporte e os campos de filtro. Por exemplo, hello instrução a seguir retorna Olá top 10 registros entre 1º de julho de 2016 e 6 de julho de 2016:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Operadores com suporte**: eq, ge, le, gt, lt

**Exemplo**:

Como usar uma data específica

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Como usar um intervalo de datas    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Observações**:

Olá datetime deveria estar no formato UTC de saudação 

- - -
### <a name="userid"></a>userId
**Operadores com suporte**: eq

**Exemplo**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Observações**:

valor de saudação do userId é um valor de cadeia de caracteres

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Operadores com suporte**: eq

**Exemplo**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Observações**:

valor de saudação do userPrincipalName é um valor de cadeia de caracteres

- - -
### <a name="appid"></a>appId
**Operadores com suporte**: eq

**Exemplo**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Observações**:

valor de saudação do appId é um valor de cadeia de caracteres

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operadores com suporte**: eq

**Exemplo**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Observações**:

valor de saudação do appDisplayName é um valor de cadeia de caracteres

- - -
### <a name="loginstatus"></a>loginStatus
**Operadores com suporte**: eq

**Exemplo**:

    $filter=loginStatus+eq+'1'  


**Observações**:

Há duas opções para o status de logon Olá: 0 - êxito, 1 - Falha

- - -
## <a name="next-steps"></a>Próximas etapas
* Você deseja toosee exemplos para atividades filtradas entrar? Check-out Olá [exemplos de API de relatório de atividade de entrada do Active Directory do Azure](active-directory-reporting-api-sign-in-activity-samples.md).
* Você deseja tooknow mais sobre a API de relatório de saudação do AD do Azure? Consulte [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).

