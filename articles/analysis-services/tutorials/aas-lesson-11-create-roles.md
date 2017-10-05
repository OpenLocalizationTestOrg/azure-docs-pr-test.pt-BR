---
title: "Lição 11 do tutorial do Azure Analysis Services: criar funções | Microsoft Docs"
description: "Descreve como criar funções no projeto de tutorial do Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="98337-103">Lição 11: criar funções</span><span class="sxs-lookup"><span data-stu-id="98337-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="98337-104">Nesta lição, você cria funções.</span><span class="sxs-lookup"><span data-stu-id="98337-104">In this lesson, you create roles.</span></span> <span data-ttu-id="98337-105">As funções fornecem segurança de dados e objetos de modelo de banco de dados, limitando o acesso aos usuários somente àqueles usuários que são membros da função.</span><span class="sxs-lookup"><span data-stu-id="98337-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="98337-106">Cada função é definida com uma única permissão: Nenhum, Leitura, Leitura e Processo, Processo ou Administrador.</span><span class="sxs-lookup"><span data-stu-id="98337-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="98337-107">Funções podem ser definidas durante a criação do modelo usando o Gerenciador de Funções.</span><span class="sxs-lookup"><span data-stu-id="98337-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="98337-108">Depois que um modelo tiver sido implantado, você poderá gerenciar funções usando o SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="98337-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="98337-109">Para saber mais, consulte [Funções](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="98337-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="98337-110">Não é necessário criar funções para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="98337-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="98337-111">Por padrão, a conta com a qual você está conectado terá privilégios de Administrador no modelo.</span><span class="sxs-lookup"><span data-stu-id="98337-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="98337-112">No entanto, para permitir que outros usuários na sua organização procurem usando um cliente de relatório, você deve criar pelo menos uma função com permissões de Leitura e adicionar esses usuários como membros.</span><span class="sxs-lookup"><span data-stu-id="98337-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="98337-113">Você cria três funções:</span><span class="sxs-lookup"><span data-stu-id="98337-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="98337-114">**Gerente de Vendas** – essa função pode incluir usuários em sua organização para os quais você deseja ter permissão de Leitura para todos os objetos de modelo e dados.</span><span class="sxs-lookup"><span data-stu-id="98337-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="98337-115">**Analista de Vendas dos EUA** – essa função pode incluir usuários em sua organização para os quais você deseja apenas ser capaz de procurar dados relacionados a vendas nos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="98337-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="98337-116">Para essa função, você usará uma fórmula DAX para definir um *Filtro de Linha*, que restringe os membros para procurar dados apenas para os Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="98337-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="98337-117">**Administrador** – essa função pode incluir usuários para os quais você deseja ter permissão de Administrador, que fornece acesso ilimitado e permissões para executar tarefas administrativas no modelo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="98337-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="98337-118">Já que as contas de usuário e de grupo do Windows em sua organização são exclusivas, você pode adicionar contas da sua organização privada para membros.</span><span class="sxs-lookup"><span data-stu-id="98337-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="98337-119">No entanto, para este tutorial, você também pode deixar os membros em branco.</span><span class="sxs-lookup"><span data-stu-id="98337-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="98337-120">Você testará o efeito de cada função posteriormente na Lição 12: Analisar no Excel.</span><span class="sxs-lookup"><span data-stu-id="98337-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="98337-121">Tempo estimado para conclusão desta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="98337-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="98337-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="98337-122">Prerequisites</span></span>  
<span data-ttu-id="98337-123">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="98337-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="98337-124">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="98337-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="98337-125">Criar funções</span><span class="sxs-lookup"><span data-stu-id="98337-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="98337-126">Para criar uma função de usuário de Gerente de Vendas</span><span class="sxs-lookup"><span data-stu-id="98337-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="98337-127">No Gerenciador de Modelos tabular, clique com o botão direito do mouse em **Funções** > **Funções**.</span><span class="sxs-lookup"><span data-stu-id="98337-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="98337-128">No Gerenciador de Funções, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="98337-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="98337-129">Clique na nova função e, na coluna **Nome**, renomeie a função para **Gerente de Vendas**.</span><span class="sxs-lookup"><span data-stu-id="98337-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="98337-130">Na coluna **Permissões**, clique na lista suspensa e, em seguida, selecione a permissão **Leitura**.</span><span class="sxs-lookup"><span data-stu-id="98337-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="98337-132">Opcional: clique na guia **Membros** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="98337-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="98337-133">Na caixa de diálogo **Selecionar Usuários ou Grupos**, digite os grupos os usuários do Windows da sua organização que você deseja incluir na função.</span><span class="sxs-lookup"><span data-stu-id="98337-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="98337-134">Para criar uma função de usuário de Analista de Vendas dos EUA</span><span class="sxs-lookup"><span data-stu-id="98337-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="98337-135">No Gerenciador de Funções, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="98337-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="98337-136">Renomeie a função para **Analista de Vendas dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="98337-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="98337-137">Dê a essa função a permissão **Leitura**.</span><span class="sxs-lookup"><span data-stu-id="98337-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="98337-138">Clique na guia Filtros de Linha e, em seguida, somente para a tabela **DimGeography**, na coluna Filtro DAX, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="98337-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="98337-139">Uma fórmula de Filtro de Linha deve ser resolvida para um valor booliano (TRUE/FALSE).</span><span class="sxs-lookup"><span data-stu-id="98337-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="98337-140">Com esta fórmula, você está especificando que somente as linhas com o valor de Código do País/Região "US" estarão visíveis para o usuário.</span><span class="sxs-lookup"><span data-stu-id="98337-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="98337-142">Opcional: clique na guia **Membros** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="98337-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="98337-143">Na caixa de diálogo **Selecionar Usuários ou Grupos**, digite os grupos os usuários do Windows da sua organização que você deseja incluir na função.</span><span class="sxs-lookup"><span data-stu-id="98337-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="98337-144">Para criar uma função de usuário Administrador</span><span class="sxs-lookup"><span data-stu-id="98337-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="98337-145">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="98337-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="98337-146">Renomeie a função para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="98337-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="98337-147">Dê permissão de **Administrador** a essa função.</span><span class="sxs-lookup"><span data-stu-id="98337-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="98337-148">Opcional: clique na guia **Membros** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="98337-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="98337-149">Na caixa de diálogo **Selecionar Usuários ou Grupos**, digite os grupos os usuários do Windows da sua organização que você deseja incluir na função.</span><span class="sxs-lookup"><span data-stu-id="98337-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="98337-150">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="98337-150">What's next?</span></span>
<span data-ttu-id="98337-151">[Lição 12: Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="98337-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
