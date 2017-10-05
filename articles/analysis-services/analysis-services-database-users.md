---
title: "Gerenciar usuários e funções de banco de dados no Azure Analysis Services | Microsoft Docs"
description: "Saiba como gerenciar usuários e funções de banco de dados em um servidor do Analysis Services no Azure."
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
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="05390-103">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="05390-103">Manage database roles and users</span></span>

<span data-ttu-id="05390-104">No nível do modelo de banco de dados, todos os usuários devem pertencer a uma função.</span><span class="sxs-lookup"><span data-stu-id="05390-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="05390-105">As funções definem os usuários com permissões específicas para o modelo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="05390-106">Qualquer usuário ou grupo de segurança adicionado a uma função deve ter uma conta em um locatário do Azure AD na mesma assinatura que o servidor.</span><span class="sxs-lookup"><span data-stu-id="05390-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="05390-107">Como você define as funções é diferente dependendo da ferramenta usada, mas o efeito é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="05390-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="05390-108">As permissões de função incluem:</span><span class="sxs-lookup"><span data-stu-id="05390-108">Role permissions include:</span></span>
*  <span data-ttu-id="05390-109">**Administrador** – os usuários têm permissões completas para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="05390-110">Funções de banco de dados com permissões de administrador são diferentes dos administradores do servidor.</span><span class="sxs-lookup"><span data-stu-id="05390-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="05390-111">**Processar** – os usuários podem se conectar e executar operações de processo no banco de dados e analisar os dados do modelo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="05390-112">**Leitura** – os usuários podem usar um aplicativo cliente para se conectar e analisar os dados do modelo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="05390-113">Ao criar um projeto de modelo tabular, você cria funções e adiciona usuários ou grupos a essas funções usando o Gerenciador de Funções no SSDT.</span><span class="sxs-lookup"><span data-stu-id="05390-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="05390-114">Quando implantado em um servidor, você usa o SSMS, [cmdlets do PowerShell para Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx) ou [TMSL](https://msdn.microsoft.com/library/mt614797.aspx) (Linguagem de Scripts do Modelo Tabular) para adicionar ou remover funções e membros de usuário.</span><span class="sxs-lookup"><span data-stu-id="05390-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="05390-115">Para adicionar ou gerenciar funções e usuários no SSDT</span><span class="sxs-lookup"><span data-stu-id="05390-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="05390-116">No SSDT > **Gerenciador de Modelos Tabular**, clique com o botão direito do mouse em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="05390-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="05390-117">No **Gerenciador de Funções**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="05390-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="05390-118">Digite um nome para a função.</span><span class="sxs-lookup"><span data-stu-id="05390-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="05390-119">Por padrão, o nome da função padrão será numerado incrementalmente para cada nova função.</span><span class="sxs-lookup"><span data-stu-id="05390-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="05390-120">É recomendável que você digite um nome que claramente Identifique o tipo de membro, por exemplo, Gerentes Financeiros ou Especialistas de Recursos Humanos.</span><span class="sxs-lookup"><span data-stu-id="05390-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="05390-121">Selecione uma das seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="05390-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="05390-122">Permissão</span><span class="sxs-lookup"><span data-stu-id="05390-122">Permission</span></span>|<span data-ttu-id="05390-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="05390-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="05390-124">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="05390-124">**None**</span></span>|<span data-ttu-id="05390-125">Os membros não podem modificar o esquema do modelo e não podem consultar dados.</span><span class="sxs-lookup"><span data-stu-id="05390-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="05390-126">**Ler**</span><span class="sxs-lookup"><span data-stu-id="05390-126">**Read**</span></span>|<span data-ttu-id="05390-127">Os membros podem consultar dados (com base em filtros de linha), mas não podem modificar o esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="05390-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="05390-128">**Ler e Processar**</span><span class="sxs-lookup"><span data-stu-id="05390-128">**Read and Process**</span></span>|<span data-ttu-id="05390-129">Os membros podem consultar dados (com base em filtros de nível de linha) e executar as operações Processar e Processar Tudo, mas não podem modificar o esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="05390-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="05390-130">**Processo**</span><span class="sxs-lookup"><span data-stu-id="05390-130">**Process**</span></span>|<span data-ttu-id="05390-131">Os membros podem executar as operações Processar e Processar Tudo.</span><span class="sxs-lookup"><span data-stu-id="05390-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="05390-132">Não podem modificar o esquema do modelo e não podem consultar dados.</span><span class="sxs-lookup"><span data-stu-id="05390-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="05390-133">**Administrador**</span><span class="sxs-lookup"><span data-stu-id="05390-133">**Administrator**</span></span>|<span data-ttu-id="05390-134">Os membros podem modificar o esquema de modelo e consultar todos os dados.</span><span class="sxs-lookup"><span data-stu-id="05390-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="05390-135">Se a função que você está criando tem a permissão Ler ou Ler e Processar, é possível adicionar filtros de linha usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="05390-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="05390-136">Clique na guia **Filtros de Linha**, selecione uma tabela, clique no campo **Filtro DAX** e digite uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="05390-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="05390-137">Clique em **Membros** > **Adicionar Externo**.</span><span class="sxs-lookup"><span data-stu-id="05390-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="05390-138">Em **Adicionar Membro Externo**, insira usuários ou grupos no seu locatário do Azure AD pelo endereço de email.</span><span class="sxs-lookup"><span data-stu-id="05390-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="05390-139">Depois que você clicar em OK e fechar o Gerenciador de Funções, as funções e membros da função aparecem no Gerenciador de Modelos Tabular.</span><span class="sxs-lookup"><span data-stu-id="05390-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Funções e usuários no Gerenciador de Modelos Tabular](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="05390-141">Implante em seu servidor do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="05390-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="05390-142">Para adicionar ou gerenciar funções e usuários no SSMS</span><span class="sxs-lookup"><span data-stu-id="05390-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="05390-143">Para adicionar funções e usuários a um modelo de banco de dados implantado, você deve estar conectado ao servidor como Administrador do servidor ou já estar em uma função de banco de dados com permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="05390-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="05390-144">No Pesquisador de Objetos, clique com o botão direito do mouse em **Funções** > **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="05390-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="05390-145">Em **Criar Função**, insira um nome de função e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="05390-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="05390-146">Selecione uma permissão.</span><span class="sxs-lookup"><span data-stu-id="05390-146">Select a permission.</span></span>
   |<span data-ttu-id="05390-147">Permissão</span><span class="sxs-lookup"><span data-stu-id="05390-147">Permission</span></span>|<span data-ttu-id="05390-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="05390-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="05390-149">**Controle total (Administrador)**</span><span class="sxs-lookup"><span data-stu-id="05390-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="05390-150">Os membros podem modificar o esquema de modelo, processar e consultar todos os dados.</span><span class="sxs-lookup"><span data-stu-id="05390-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="05390-151">**Processar banco de dados**</span><span class="sxs-lookup"><span data-stu-id="05390-151">**Process database**</span></span>|<span data-ttu-id="05390-152">Os membros podem executar as operações Processar e Processar Tudo.</span><span class="sxs-lookup"><span data-stu-id="05390-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="05390-153">Não podem modificar o esquema do modelo e não podem consultar dados.</span><span class="sxs-lookup"><span data-stu-id="05390-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="05390-154">**Ler**</span><span class="sxs-lookup"><span data-stu-id="05390-154">**Read**</span></span>|<span data-ttu-id="05390-155">Os membros podem consultar dados (com base em filtros de linha), mas não podem modificar o esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="05390-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="05390-156">Clique em **Associação**, em seguida, insira um usuário ou grupo no seu locatário do Azure AD pelo endereço de email.</span><span class="sxs-lookup"><span data-stu-id="05390-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Adicionar usuário](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="05390-158">Se a função que você está criando tem a permissão Ler, é possível adicionar filtros de linha usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="05390-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="05390-159">Clique em **Filtros de Linha**, selecione uma tabela e, em seguida, digite uma fórmula DAX no campo **Filtro DAX**.</span><span class="sxs-lookup"><span data-stu-id="05390-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="05390-160">Para adicionar funções e usuários usando um script TMSL</span><span class="sxs-lookup"><span data-stu-id="05390-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="05390-161">Você pode executar um script TMSL na janela XMLA no SSMS ou usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05390-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="05390-162">Use o comando [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) e o objeto [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl).</span><span class="sxs-lookup"><span data-stu-id="05390-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="05390-163">**Exemplo de script TMSL**</span><span class="sxs-lookup"><span data-stu-id="05390-163">**Sample TMSL script**</span></span>

<span data-ttu-id="05390-164">Neste exemplo, um usuário externo B2B e um grupo são adicionados à função Analista com permissões de leitura para o banco de dados SalesBI.</span><span class="sxs-lookup"><span data-stu-id="05390-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="05390-165">O usuário externo e o grupo devem estar no mesmo locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05390-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="05390-166">Para adicionar funções e usuários usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="05390-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="05390-167">O módulo [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) fornece cmdlets de gerenciamento de banco de dados de tarefas específicas e o cmdlet Invoke-ASCmd de uso geral, que aceita um script ou consulta de TMSL (Linguagem de Script de Modelo Tabular).</span><span class="sxs-lookup"><span data-stu-id="05390-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="05390-168">Os cmdlets a seguir são usados para gerenciar usuários e funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="05390-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="05390-169">Cmdlet</span></span>|<span data-ttu-id="05390-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="05390-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="05390-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="05390-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="05390-172">Adicionar um membro a uma função de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="05390-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="05390-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="05390-174">Remover um membro de uma função de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="05390-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="05390-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="05390-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="05390-176">Executar um script TMSL.</span><span class="sxs-lookup"><span data-stu-id="05390-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="05390-177">Filtros de linha</span><span class="sxs-lookup"><span data-stu-id="05390-177">Row filters</span></span>  
<span data-ttu-id="05390-178">Os filtros de linha definem quais linhas em uma tabela podem ser consultadas por membros de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="05390-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="05390-179">Os filtros de linha são definidos para cada tabela em um modelo usando fórmulas DAX.</span><span class="sxs-lookup"><span data-stu-id="05390-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="05390-180">Os filtros de linha podem ser definidos somente para funções com as permissões Ler e Ler e Processar.</span><span class="sxs-lookup"><span data-stu-id="05390-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="05390-181">Por padrão, se um filtro de linha não está definido para uma tabela específica, os membros podem consultar todas as linhas na tabela, a menos que a filtragem cruzada se aplique de outra tabela.</span><span class="sxs-lookup"><span data-stu-id="05390-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="05390-182">Os filtros de linha exigem uma fórmula DAX, que deve ser avaliada como um valor TRUE/FALSE, para definir as linhas que podem ser consultadas por membros daquela função específica.</span><span class="sxs-lookup"><span data-stu-id="05390-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="05390-183">Não é possível consultar linhas não incluídas na fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="05390-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="05390-184">Por exemplo, a tabela Customers com a seguinte expressão de filtros de linha, *=Customers [Country] = “USA”*, os membros da função Sales podem ver apenas os clientes nos EUA.</span><span class="sxs-lookup"><span data-stu-id="05390-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="05390-185">Os filtros de linha são aplicados às linhas especificadas e às linhas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="05390-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="05390-186">Quando uma tabela tem várias relações, os filtros aplicam segurança para a relação que está ativa.</span><span class="sxs-lookup"><span data-stu-id="05390-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="05390-187">Os filtros de linha são interseccionados com outros filtros de linha definidos para tabelas relacionadas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05390-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="05390-188">Tabela</span><span class="sxs-lookup"><span data-stu-id="05390-188">Table</span></span>|<span data-ttu-id="05390-189">Expressão DAX</span><span class="sxs-lookup"><span data-stu-id="05390-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="05390-190">Região</span><span class="sxs-lookup"><span data-stu-id="05390-190">Region</span></span>|<span data-ttu-id="05390-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="05390-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="05390-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="05390-192">ProductCategory</span></span>|<span data-ttu-id="05390-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="05390-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="05390-194">Transações</span><span class="sxs-lookup"><span data-stu-id="05390-194">Transactions</span></span>|<span data-ttu-id="05390-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="05390-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="05390-196">O efeito líquido é que os membros podem consultar as linhas de dados em que o cliente está nos EUA, a categoria de produto é bicicletas e o ano é 2016.</span><span class="sxs-lookup"><span data-stu-id="05390-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="05390-197">Os usuários não podem consultar transações fora dos EUA, transações que não são bicicletas ou transações que não são em 2016 amenos que sejam um membro de outra função que concede essas permissões.</span><span class="sxs-lookup"><span data-stu-id="05390-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="05390-198">Você pode usar o filtro, *=FALSE()*, para negar o acesso a todas as linhas de uma tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="05390-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05390-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05390-199">Next steps</span></span>
  <span data-ttu-id="05390-200">[Gerenciar administradores de servidor](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="05390-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="05390-201">Gerenciar o Azure Analysis Services com PowerShell</span><span class="sxs-lookup"><span data-stu-id="05390-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="05390-202">Referência de TMSL (Linguagem de Scripts do Modelo Tabular)</span><span class="sxs-lookup"><span data-stu-id="05390-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

