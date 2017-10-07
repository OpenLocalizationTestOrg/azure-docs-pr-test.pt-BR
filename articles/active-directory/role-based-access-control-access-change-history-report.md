---
title: "relatórios de aaaAccess - RBAC do Azure | Microsoft Docs"
description: "Gere um relatório que lista todas as alterações no acesso tooyour assinaturas do Azure com controle de acesso baseado em função sobre Olá últimos 90 dias."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Criar um relatório de acesso para o Controle de Acesso Baseado em Função
Sempre que alguém concede ou nega acesso dentro de suas assinaturas, alterações de saudação são registradas nos eventos do Azure. Você pode criar acesso toosee de relatórios de histórico de alteração de todas as alterações para Olá últimos 90 dias.

## <a name="create-a-report-with-azure-powershell"></a>Criar um relatório com o Azure PowerShell
toocreate um acesso de alterar o relatório de histórico no PowerShell, use Olá [AzureRMAuthorizationChangeLog Get](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.

Quando você chamar esse comando, você pode especificar qual propriedade de atribuições de saudação desejado na lista, incluindo Olá a seguir:

| Propriedade | Descrição |
| --- | --- |
| **Ação** |Se o acesso foi concedido ou revogado |
| **Chamador** |Olá proprietário responsável por acesso Olá alterar |
| **PrincipalId** | Identificador exclusivo de saudação do usuário hello, grupo ou aplicativo que foi atribuído a função hello |
| **PrincipalName** |nome de saudação do usuário hello, grupo ou aplicativo |
| **PrincipalType** |Se a atribuição de saudação foi para um usuário, grupo ou aplicativo |
| **RoleDefinitionId** |Olá GUID da função hello que foi concedida ou revogada |
| **RoleName** |função Hello que foi concedida ou revogada |
| **Escopo** | Identificador exclusivo de saudação da assinatura hello, grupo de recursos ou recurso que Olá atribuição aplica-se muito| 
| **ScopeName** |nome de saudação de assinatura hello, grupo de recursos ou recurso |
| **ScopeType** |Se a atribuição de saudação foi no escopo do recurso, grupo de recursos ou assinatura Olá |
| **Timestamp** |saudação de data e hora que o acesso foi alterado |

Este exemplo de comando lista todas as alterações de acesso em assinatura Olá Olá últimos sete dias:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - captura de tela](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Criar um relatório com a CLI do Azure
toocreate um relatório de histórico de alteração de acesso em hello Azure interface de linha de comando (CLI), use Olá `azure role assignment changelog list` comando.

## <a name="export-tooa-spreadsheet"></a>Exportar tooa planilha
toosave Olá relatório ou manipular dados hello, exportação Olá acesso alterações em um arquivo. csv. Em seguida, você pode exibir o relatório de saudação em uma planilha para análise.

![Log de alteração exibido como planilha - captura de tela](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Próximas etapas
* Trabalhe com [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)
* Saiba como toomanage [RBAC do Azure com o powershell](role-based-access-control-manage-access-powershell.md)

