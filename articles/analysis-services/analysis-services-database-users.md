---
title: "banco de dados ao aaaManage, funções e usuários no Azure Analysis Services | Microsoft Docs"
description: "Saiba como toomanage banco de dados funções e usuários em um servidor do Analysis Services no Azure."
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="54081-103">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="54081-103">Manage database roles and users</span></span>

<span data-ttu-id="54081-104">No nível de banco de dados de modelo hello, todos os usuários devem pertencer a função tooa.</span><span class="sxs-lookup"><span data-stu-id="54081-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="54081-105">As funções definem os usuários com permissões específicas para o banco de dados de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="54081-106">Qualquer usuário ou grupo de segurança adicionadas tooa função deve ter uma conta em um locatário do AD do Azure no hello mesma assinatura que o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="54081-107">Como definir funções é diferente dependendo ferramenta Olá usada, mas efeito Olá é Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="54081-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="54081-108">As permissões de função incluem:</span><span class="sxs-lookup"><span data-stu-id="54081-108">Role permissions include:</span></span>
*  <span data-ttu-id="54081-109">**Administrador** -os usuários têm permissões completas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="54081-110">Funções de banco de dados com permissões de administrador são diferentes dos administradores do servidor.</span><span class="sxs-lookup"><span data-stu-id="54081-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="54081-111">**Processo** -os usuários podem se conectar a tooand executar operações de processo no banco de dados de saudação e analisar dados de banco de dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="54081-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="54081-112">**Leitura** -os usuários podem usar um cliente de aplicativo tooconnect tooand analisar dados de banco de dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="54081-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="54081-113">Ao criar um projeto de modelo de tabela, você pode criar funções e adiciona usuários ou grupos de funções de toothose usando o Gerenciador de funções no SSDT.</span><span class="sxs-lookup"><span data-stu-id="54081-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="54081-114">Quando implantado tooa server, você usa o SSMS, [cmdlets do PowerShell do Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), ou [linguagem de script de modelo de tabela](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) ou remover funções e membros de usuário.</span><span class="sxs-lookup"><span data-stu-id="54081-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="54081-115">tooadd ou gerenciar funções e usuários no SSDT</span><span class="sxs-lookup"><span data-stu-id="54081-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="54081-116">No SSDT > **Gerenciador de Modelos Tabular**, clique com o botão direito do mouse em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="54081-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="54081-117">No **Gerenciador de Funções**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="54081-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="54081-118">Digite um nome para a função hello.</span><span class="sxs-lookup"><span data-stu-id="54081-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="54081-119">Por padrão, o nome de saudação da função de padrão de saudação é numerado incrementalmente para cada nova função.</span><span class="sxs-lookup"><span data-stu-id="54081-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="54081-120">É recomendável que você digite um nome que claramente Identifique o tipo de membro hello, por exemplo, gerentes financeiros ou especialistas de recursos humanos.</span><span class="sxs-lookup"><span data-stu-id="54081-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="54081-121">Selecione uma saudação as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="54081-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="54081-122">Permissão</span><span class="sxs-lookup"><span data-stu-id="54081-122">Permission</span></span>|<span data-ttu-id="54081-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="54081-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="54081-124">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="54081-124">**None**</span></span>|<span data-ttu-id="54081-125">Membros não é possível modificar o esquema de modelo hello e não é possível consultar dados.</span><span class="sxs-lookup"><span data-stu-id="54081-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="54081-126">**Ler**</span><span class="sxs-lookup"><span data-stu-id="54081-126">**Read**</span></span>|<span data-ttu-id="54081-127">Os membros podem consultar dados (com base em filtros de linha) mas não é possível modificar o esquema de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="54081-128">**Ler e Processar**</span><span class="sxs-lookup"><span data-stu-id="54081-128">**Read and Process**</span></span>|<span data-ttu-id="54081-129">Os membros podem consultar dados (com base em filtros de nível de linha) e executadas operações de processar e processar tudo, mas não é possível modificar o esquema de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="54081-130">**Processo**</span><span class="sxs-lookup"><span data-stu-id="54081-130">**Process**</span></span>|<span data-ttu-id="54081-131">Os membros podem executar as operações Processar e Processar Tudo.</span><span class="sxs-lookup"><span data-stu-id="54081-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="54081-132">Não é possível modificar o esquema de modelo hello e não é possível consultar dados.</span><span class="sxs-lookup"><span data-stu-id="54081-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="54081-133">**Administrador**</span><span class="sxs-lookup"><span data-stu-id="54081-133">**Administrator**</span></span>|<span data-ttu-id="54081-134">Os membros podem modificar o esquema de modelo Olá e consultar todos os dados.</span><span class="sxs-lookup"><span data-stu-id="54081-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="54081-135">Se a função hello que você está criando leu ou permissão de leitura e processo, você pode adicionar filtros de linha usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="54081-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="54081-136">Clique em Olá **filtros de linha** guia, selecione uma tabela, clique Olá **filtro DAX** campo e, em seguida, digite uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="54081-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="54081-137">Clique em **Membros** > **Adicionar Externo**.</span><span class="sxs-lookup"><span data-stu-id="54081-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="54081-138">Em **Adicionar Membro Externo**, insira usuários ou grupos no seu locatário do Azure AD pelo endereço de email.</span><span class="sxs-lookup"><span data-stu-id="54081-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="54081-139">Depois que você clicar em OK e fechar o Gerenciador de Funções, as funções e membros da função aparecem no Gerenciador de Modelos Tabular.</span><span class="sxs-lookup"><span data-stu-id="54081-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Funções e usuários no Gerenciador de Modelos Tabular](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="54081-141">Implante o servidor de serviços de análise do Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="54081-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="54081-142">tooadd ou gerenciar funções e usuários no SSMS</span><span class="sxs-lookup"><span data-stu-id="54081-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="54081-143">tooadd tooa de usuários e funções implantadas banco de dados modelo, você deve ser o servidor toohello conectado como um administrador de servidor ou já está em uma função de banco de dados com permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="54081-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="54081-144">No Pesquisador de Objetos, clique com o botão direito do mouse em **Funções** > **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="54081-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="54081-145">Em **Criar Função**, insira um nome de função e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="54081-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="54081-146">Selecione uma permissão.</span><span class="sxs-lookup"><span data-stu-id="54081-146">Select a permission.</span></span>
   |<span data-ttu-id="54081-147">Permissão</span><span class="sxs-lookup"><span data-stu-id="54081-147">Permission</span></span>|<span data-ttu-id="54081-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="54081-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="54081-149">**Controle total (Administrador)**</span><span class="sxs-lookup"><span data-stu-id="54081-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="54081-150">Os membros podem modificar o esquema de modelo hello, processar e consultar todos os dados.</span><span class="sxs-lookup"><span data-stu-id="54081-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="54081-151">**Processar banco de dados**</span><span class="sxs-lookup"><span data-stu-id="54081-151">**Process database**</span></span>|<span data-ttu-id="54081-152">Os membros podem executar as operações Processar e Processar Tudo.</span><span class="sxs-lookup"><span data-stu-id="54081-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="54081-153">Não é possível modificar o esquema de modelo hello e não é possível consultar dados.</span><span class="sxs-lookup"><span data-stu-id="54081-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="54081-154">**Ler**</span><span class="sxs-lookup"><span data-stu-id="54081-154">**Read**</span></span>|<span data-ttu-id="54081-155">Os membros podem consultar dados (com base em filtros de linha) mas não é possível modificar o esquema de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="54081-156">Clique em **Associação**, em seguida, insira um usuário ou grupo no seu locatário do Azure AD pelo endereço de email.</span><span class="sxs-lookup"><span data-stu-id="54081-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Adicionar usuário](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="54081-158">Se a função hello que está criando tem permissão de leitura, você pode adicionar filtros de linha usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="54081-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="54081-159">Clique em **filtros de linha**, selecione uma tabela e, em seguida, digite uma fórmula DAX Olá **filtro DAX** campo.</span><span class="sxs-lookup"><span data-stu-id="54081-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="54081-160">tooadd funções e usuários usando um script TMSL</span><span class="sxs-lookup"><span data-stu-id="54081-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="54081-161">Você pode executar um script TMSL na janela XMLA Olá no SSMS ou usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54081-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="54081-162">Saudação de uso [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) comando e hello [funções](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objeto.</span><span class="sxs-lookup"><span data-stu-id="54081-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="54081-163">**Exemplo de script TMSL**</span><span class="sxs-lookup"><span data-stu-id="54081-163">**Sample TMSL script**</span></span>

<span data-ttu-id="54081-164">Neste exemplo, um usuário externo B2B e um grupo são adicionados toohello a função de analista com permissões de leitura para o banco de dados do hello SalesBI.</span><span class="sxs-lookup"><span data-stu-id="54081-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="54081-165">Ambos Olá usuário externo e o grupo deve estar no mesmo locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="54081-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
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

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="54081-166">tooadd funções e usuários usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="54081-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="54081-167">Olá [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) módulo fornece banco de dados específicos de tarefa gerenciamento cmdlets e hello geral cmdlet Invoke-ASCmd que aceita uma consulta de linguagem de script de modelo Tabular (TMSL) ou um script.</span><span class="sxs-lookup"><span data-stu-id="54081-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="54081-168">Olá cmdlets a seguir é usado para gerenciar usuários e funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="54081-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="54081-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="54081-169">Cmdlet</span></span>|<span data-ttu-id="54081-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="54081-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="54081-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="54081-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="54081-172">Adicione um membro da função de banco de dados tooa.</span><span class="sxs-lookup"><span data-stu-id="54081-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="54081-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="54081-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="54081-174">Remover um membro de uma função de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="54081-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="54081-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="54081-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="54081-176">Executar um script TMSL.</span><span class="sxs-lookup"><span data-stu-id="54081-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="54081-177">Filtros de linha</span><span class="sxs-lookup"><span data-stu-id="54081-177">Row filters</span></span>  
<span data-ttu-id="54081-178">Os filtros de linha definem quais linhas em uma tabela podem ser consultadas por membros de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="54081-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="54081-179">Os filtros de linha são definidos para cada tabela em um modelo usando fórmulas DAX.</span><span class="sxs-lookup"><span data-stu-id="54081-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="54081-180">Os filtros de linha podem ser definidos somente para funções com as permissões Ler e Ler e Processar.</span><span class="sxs-lookup"><span data-stu-id="54081-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="54081-181">Por padrão, se um filtro de linha não está definido para uma tabela específica, membros podem consultar todas as linhas na tabela hello, a menos que a filtragem cruzada se aplica de outra tabela.</span><span class="sxs-lookup"><span data-stu-id="54081-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="54081-182">Os filtros de linha exigem uma fórmula DAX, que deve ser avaliada tooa valor TRUE/FALSE, linhas de saudação toodefine que podem ser consultadas por membros daquela função específica.</span><span class="sxs-lookup"><span data-stu-id="54081-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="54081-183">Não não possível consultar as linhas não incluídas na fórmula DAX de saudação.</span><span class="sxs-lookup"><span data-stu-id="54081-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="54081-184">Por exemplo, Olá tabela Customers com hello expressão de filtros de linha, a seguir *= clientes [País] = "EUA"*, membros da função de vendas Olá só podem consultar clientes nos Olá EUA.</span><span class="sxs-lookup"><span data-stu-id="54081-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="54081-185">Filtros de linha aplicam toohello especificado linhas e linhas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="54081-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="54081-186">Quando uma tabela tiver várias relações, os filtros aplicam segurança para a relação de saudação que está ativa.</span><span class="sxs-lookup"><span data-stu-id="54081-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="54081-187">Os filtros de linha são interseccionados com outros filtros de linha definidos para tabelas relacionadas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54081-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="54081-188">Tabela</span><span class="sxs-lookup"><span data-stu-id="54081-188">Table</span></span>|<span data-ttu-id="54081-189">Expressão DAX</span><span class="sxs-lookup"><span data-stu-id="54081-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="54081-190">Região</span><span class="sxs-lookup"><span data-stu-id="54081-190">Region</span></span>|<span data-ttu-id="54081-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="54081-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="54081-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="54081-192">ProductCategory</span></span>|<span data-ttu-id="54081-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="54081-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="54081-194">Transações</span><span class="sxs-lookup"><span data-stu-id="54081-194">Transactions</span></span>|<span data-ttu-id="54081-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="54081-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="54081-196">efeito de saudação é membros podem consultar as linhas de dados em que cliente hello está nos EUA hello, Olá categoria de produto for bicicletas e ano Olá é 2016.</span><span class="sxs-lookup"><span data-stu-id="54081-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="54081-197">Os usuários não podem consultar transações fora do EUA hello, transações que não são Bicicletas ou transações não 2016, a menos que fossem membros de outra função que concede estas permissões.</span><span class="sxs-lookup"><span data-stu-id="54081-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="54081-198">Você pode usar o filtro de saudação *=FALSE()*, toodeny acessem as linhas tooall para uma tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="54081-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54081-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54081-199">Next steps</span></span>
  <span data-ttu-id="54081-200">[Gerenciar administradores de servidor](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="54081-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="54081-201">Gerenciar o Azure Analysis Services com PowerShell</span><span class="sxs-lookup"><span data-stu-id="54081-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="54081-202">Referência de TMSL (Linguagem de Scripts do Modelo Tabular)</span><span class="sxs-lookup"><span data-stu-id="54081-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

