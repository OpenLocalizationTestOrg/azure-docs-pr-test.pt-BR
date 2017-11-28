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
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="d9bda-103">Criar um relatório de acesso para o Controle de Acesso Baseado em Função</span><span class="sxs-lookup"><span data-stu-id="d9bda-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="d9bda-104">Sempre que alguém concede ou nega acesso dentro de suas assinaturas, alterações de saudação são registradas nos eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bda-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="d9bda-105">Você pode criar acesso toosee de relatórios de histórico de alteração de todas as alterações para Olá últimos 90 dias.</span><span class="sxs-lookup"><span data-stu-id="d9bda-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="d9bda-106">Criar um relatório com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9bda-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="d9bda-107">toocreate um acesso de alterar o relatório de histórico no PowerShell, use Olá [AzureRMAuthorizationChangeLog Get](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.</span><span class="sxs-lookup"><span data-stu-id="d9bda-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="d9bda-108">Quando você chamar esse comando, você pode especificar qual propriedade de atribuições de saudação desejado na lista, incluindo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9bda-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="d9bda-109">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d9bda-109">Property</span></span> | <span data-ttu-id="d9bda-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="d9bda-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9bda-111">**Ação**</span><span class="sxs-lookup"><span data-stu-id="d9bda-111">**Action**</span></span> |<span data-ttu-id="d9bda-112">Se o acesso foi concedido ou revogado</span><span class="sxs-lookup"><span data-stu-id="d9bda-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="d9bda-113">**Chamador**</span><span class="sxs-lookup"><span data-stu-id="d9bda-113">**Caller**</span></span> |<span data-ttu-id="d9bda-114">Olá proprietário responsável por acesso Olá alterar</span><span class="sxs-lookup"><span data-stu-id="d9bda-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="d9bda-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="d9bda-115">**PrincipalId**</span></span> | <span data-ttu-id="d9bda-116">Identificador exclusivo de saudação do usuário hello, grupo ou aplicativo que foi atribuído a função hello</span><span class="sxs-lookup"><span data-stu-id="d9bda-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="d9bda-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="d9bda-117">**PrincipalName**</span></span> |<span data-ttu-id="d9bda-118">nome de saudação do usuário hello, grupo ou aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9bda-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="d9bda-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="d9bda-119">**PrincipalType**</span></span> |<span data-ttu-id="d9bda-120">Se a atribuição de saudação foi para um usuário, grupo ou aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9bda-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="d9bda-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="d9bda-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="d9bda-122">Olá GUID da função hello que foi concedida ou revogada</span><span class="sxs-lookup"><span data-stu-id="d9bda-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="d9bda-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="d9bda-123">**RoleName**</span></span> |<span data-ttu-id="d9bda-124">função Hello que foi concedida ou revogada</span><span class="sxs-lookup"><span data-stu-id="d9bda-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="d9bda-125">**Escopo**</span><span class="sxs-lookup"><span data-stu-id="d9bda-125">**Scope**</span></span> | <span data-ttu-id="d9bda-126">Identificador exclusivo de saudação da assinatura hello, grupo de recursos ou recurso que Olá atribuição aplica-se muito</span><span class="sxs-lookup"><span data-stu-id="d9bda-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="d9bda-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="d9bda-127">**ScopeName**</span></span> |<span data-ttu-id="d9bda-128">nome de saudação de assinatura hello, grupo de recursos ou recurso</span><span class="sxs-lookup"><span data-stu-id="d9bda-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="d9bda-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="d9bda-129">**ScopeType**</span></span> |<span data-ttu-id="d9bda-130">Se a atribuição de saudação foi no escopo do recurso, grupo de recursos ou assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="d9bda-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="d9bda-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="d9bda-131">**Timestamp**</span></span> |<span data-ttu-id="d9bda-132">saudação de data e hora que o acesso foi alterado</span><span class="sxs-lookup"><span data-stu-id="d9bda-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="d9bda-133">Este exemplo de comando lista todas as alterações de acesso em assinatura Olá Olá últimos sete dias:</span><span class="sxs-lookup"><span data-stu-id="d9bda-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - captura de tela](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="d9bda-135">Criar um relatório com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d9bda-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="d9bda-136">toocreate um relatório de histórico de alteração de acesso em hello Azure interface de linha de comando (CLI), use Olá `azure role assignment changelog list` comando.</span><span class="sxs-lookup"><span data-stu-id="d9bda-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="d9bda-137">Exportar tooa planilha</span><span class="sxs-lookup"><span data-stu-id="d9bda-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="d9bda-138">toosave Olá relatório ou manipular dados hello, exportação Olá acesso alterações em um arquivo. csv.</span><span class="sxs-lookup"><span data-stu-id="d9bda-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="d9bda-139">Em seguida, você pode exibir o relatório de saudação em uma planilha para análise.</span><span class="sxs-lookup"><span data-stu-id="d9bda-139">You can then view hello report in a spreadsheet for review.</span></span>

![Log de alteração exibido como planilha - captura de tela](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="d9bda-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9bda-141">Next steps</span></span>
* <span data-ttu-id="d9bda-142">Trabalhe com [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="d9bda-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="d9bda-143">Saiba como toomanage [RBAC do Azure com o powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d9bda-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

