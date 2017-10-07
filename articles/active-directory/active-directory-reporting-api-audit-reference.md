---
title: "auditoria de Active Directory aaaAzure Referência de API | Microsoft Docs"
description: Como tooget iniciada com hello API de auditoria do Active Directory do Azure
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Referência à API de auditoria do Azure Active Directory
Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.  
Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de auditoria usando o código ou ferramentas relacionadas.
escopo de saudação deste tópico é tooprovide você com informações de referência sobre Olá **audit API**.

Consulte:

* [Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais

* [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.


Para:

- Perguntas frequentes, leia nossas [Perguntas Frequentes](active-directory-reporting-faq.md) 

- Solucionar problemas, [registre um tíquete de suporte](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Quem pode acessar dados Olá?
* Usuários na função de administrador de segurança ou segurança leitor Olá
* Administradores globais
* Qualquer aplicativo que tenha autorização tooaccess Olá API (o autorização de aplicativo pode ser configurado somente com base na permissão do Administrador Global)

## <a name="prerequisites"></a>Pré-requisitos
Em ordem tooaccess esse relatório por meio de Olá API de relatório, você deve ter:

* Um [Azure Active Directory gratuito ou uma edição melhor](active-directory-editions.md)
* Olá concluído [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Acessando a API de saudação
É possível acessar essa API por meio de saudação [Gerenciador de gráficos](https://graphexplorer2.cloudapp.net) ou programaticamente, usando, por exemplo, do PowerShell. Para toocorrectly PowerShell interpretar a sintaxe de filtro OData Olá usada nas chamadas AAD Graph REST, você deve usar Olá acento (também conhecido como: acento grave) caractere muito "caractere de escape" hello $. caractere de acento grave Olá serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell toodo uma interpretação de literal de caractere de $ hello e evitar confundi-lo como um nome de variável do PowerShell (ou seja: $filter).

Olá foco deste tópico é Olá Gerenciador de gráficos. Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Ponto de extremidade de API
Você pode acessar essa API usando Olá URI a seguir:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Não há nenhum limite no número de saudação de registros retornados pela API de auditoria de saudação do AD do Azure (usando a paginação do OData).
Para conhecer os limites de retenção em dados de relatório, confira [Políticas de retenção de relatório](active-directory-reporting-retention.md).

Essa chamada retorna dados saudação em lotes. Cada lote tem no máximo 1000 registros.  
tooget Olá próximo lote de registros, use Olá próximo link. Obter informações de token Skip de saudação do primeiro conjunto de registros retornados de saudação. símbolo de salto Olá será final Olá Olá do conjunto de resultados.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtros com suporte
Você pode reduzir o número de saudação de registros que são retornados por uma API chamada na forma de um filtro.  
Para entrar API dados relacionados, Olá filtros a seguir têm suporte:

* **$top =\<retornado do número de registros toobe\>**  -número de saudação toolimit de registros retornados. Esta é uma operação cara. Você não deve usar esse filtro se quiser tooreturn milhares de objetos.     
* **$filter =\<sua instrução de filtro\>**  -toospecify, cada saudação de campos de filtro com suporte, tipo de saudação de registros que importam

## <a name="supported-filter-fields-and-operators"></a>Campos de filtro e operadores com suporte
tipo de saudação toospecify de registros importantes para você, você pode criar uma instrução de filtro que pode conter um ou uma combinação de saudação campos de filtro a seguir:

* [activityDate](#activitydate) – define uma data ou intervalo de datas
* [categoria](#category) -define a categoria Olá deseja toofilter no.
* [activityStatus](#activitystatus) -define o status de saudação de uma atividade
* [activityType](#activitytype) -define o tipo de saudação de uma atividade
* [atividade](#activity) -define atividade hello como cadeia de caracteres  
* [nome do ator](#actorname) -define ator Olá na forma de nome do ator Olá
* [ator/objectid](#actorobjectid) -define ator Olá na forma de ID do ator Olá   
* [ator/upn](#actorupn) -define ator Olá no formulário princípio do ator Olá nome de usuário (UPN) 
* [nome do destino](#targetname) -define o destino de saudação na forma de nome do ator Olá
* [destino/objectid](#targetobjectid) -define o destino de saudação na forma de ID do destino Olá  
* [destino/upn](#targetupn) -define ator Olá no formulário princípio do ator Olá nome de usuário (UPN)   

- - -
### <a name="activitydate"></a>activityDate
**Operadores com suporte**: eq, ge, le, gt, lt

**Exemplo**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Observações**:

datetime deve estar no formato UTC

- - -
### <a name="category"></a>categoria

**Valores com suporte**:

| Categoria                         | Valor     |
| :--                              | ---       |
| Diretório principal                   | Diretório |
| Gerenciamento de senhas de auto-atendimento | SSPR      |
| Gerenciamento de grupos de autoatendimento    | SSGM      |
| Provisionamento de conta de usuário             | Sincronizar      |
| Substituição de senha automática      | Substituição de senha automática |
| Identity Protection              | IdentityProtection |
| Usuários Convidados                    | Usuários Convidados |
| Serviço MIM                      | Serviço MIM |



**Operadores com suporte**: eq

**Exemplo**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**Valores com suporte**:

| Status da Atividade | Valor |
| :--             | ---   |
| Sucesso         | 0     |
| Failure         | - 1   |

**Operadores com suporte**: eq

**Exemplo**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Operadores com suporte**: eq

**Exemplo**:

    $filter=activityType eq 'User'    

**Observações**:

diferencia maiúsculas de minúsculas

- - -
### <a name="activity"></a>activity
**Suporte para operadores**: eq, contains, startsWith

**Exemplo**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Observações**:

diferencia maiúsculas de minúsculas

- - -
### <a name="actorname"></a>actor/name
**Suporte para operadores**: eq, contains, startsWith

**Exemplo**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Observações**:

não diferenciam maiúsculas de minúsculas

- - -
### <a name="actorobjectid"></a>actor/objectid
**Operadores com suporte**: eq

**Exemplo**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/name
**Suporte para operadores**: eq, contains, startsWith

**Exemplo**:

    $filter=targets/any(t: t/name eq 'some name')    

**Observações**:

não diferenciam maiúsculas de minúsculas

- - -
### <a name="targetupn"></a>target/upn
**Suporte para operadores**: eq, startsWith

**Exemplo**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Observações**:

* não diferenciam maiúsculas de minúsculas
* Você precisará tooadd Olá completo namespace ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>target/objectid
**Operadores com suporte**: eq

**Exemplo**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>ator/upn
**Suporte para operadores**: eq, startsWith

**Exemplo**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Observações**:

* não diferenciam maiúsculas de minúsculas 
* Você precisará tooadd Olá completo namespace ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Próximas etapas
* Você deseja toosee exemplos para atividades de sistema filtrado? Check-out Olá [exemplos de API de auditoria do Active Directory do Azure](active-directory-reporting-api-audit-samples.md).
* Você deseja tooknow mais sobre a API de relatório de saudação do AD do Azure? Consulte [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).

