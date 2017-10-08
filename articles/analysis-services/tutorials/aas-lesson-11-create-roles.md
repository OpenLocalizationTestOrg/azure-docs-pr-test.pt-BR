---
<span data-ttu-id="8cfe6-101">título: aaa "lição do tutorial do Azure Analysis Services 11: criar funções | Descrição de Microsoft Docs": descreve como funções toocreate Olá projeto do tutorial do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="8cfe6-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="8cfe6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="8cfe6-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="8cfe6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="8cfe6-104">Lição 11: criar funções</span><span class="sxs-lookup"><span data-stu-id="8cfe6-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8cfe6-105">Nesta lição, você cria funções.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-105">In this lesson, you create roles.</span></span> <span data-ttu-id="8cfe6-106">As funções fornecem segurança de dados e de objetos de banco de dados de modelo, limitando o acesso tooonly aos usuários que são membros da função.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="8cfe6-107">Cada função é definida com uma única permissão: Nenhum, Leitura, Leitura e Processo, Processo ou Administrador.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="8cfe6-108">Funções podem ser definidas durante a criação do modelo usando o Gerenciador de Funções.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="8cfe6-109">Depois que um modelo tiver sido implantado, você poderá gerenciar funções usando o SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="8cfe6-110">mais, consulte toolearn [funções](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="8cfe6-111">Criação de funções é toocomplete não é necessário neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="8cfe6-112">Por padrão, a conta Olá com que você está conectado tem privilégios de administrador no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="8cfe6-113">No entanto, para outros usuários na toobrowse sua organização usando um cliente de relatório, você deve criar pelo menos uma função com leitura permissões e adicione esses usuários como membros.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="8cfe6-114">Você cria três funções:</span><span class="sxs-lookup"><span data-stu-id="8cfe6-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="8cfe6-115">**Gerente de vendas** – essa função pode incluir usuários em sua organização para o qual você deseja toohave leitura permissão tooall objetos e dados modelo.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="8cfe6-116">**Analista de vendas dos EUA** – essa função pode incluir usuários em sua organização para o qual você deseja que apenas os dados de toobrowse capaz de toobe relacionados toosales em Olá dos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="8cfe6-117">Para essa função, você usar um toodefine de fórmula do DAX um *filtro de linha*, que restringe os membros toobrowse somente os dados do hello dos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="8cfe6-118">**Administrador** – essa função pode incluir os usuários para o qual você deseja toohave permissão de administrador, que permite acesso ilimitado e permissões de tarefas administrativas tooperform no banco de dados de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="8cfe6-119">Como contas de usuário e grupo do Windows em sua organização são exclusivas, você pode adicionar contas de toomembers sua organização.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="8cfe6-120">No entanto, para este tutorial, você também pode deixar os membros de saudação em branco.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="8cfe6-121">Testar o efeito de saudação de cada função posteriormente na lição 12: analisar no Excel.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="8cfe6-122">Estimado tempo toocomplete nesta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="8cfe6-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8cfe6-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cfe6-123">Prerequisites</span></span>  
<span data-ttu-id="8cfe6-124">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="8cfe6-125">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="8cfe6-126">Criar funções</span><span class="sxs-lookup"><span data-stu-id="8cfe6-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="8cfe6-127">toocreate uma função de usuário do gerente de vendas</span><span class="sxs-lookup"><span data-stu-id="8cfe6-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="8cfe6-128">No Gerenciador de Modelos tabular, clique com o botão direito do mouse em **Funções** > **Funções**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="8cfe6-129">No Gerenciador de Funções, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="8cfe6-130">Clique em nova função de Olá e, em seguida, em Olá **nome** coluna, renomeie a função hello muito**gerente de vendas**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="8cfe6-131">Em Olá **permissões** coluna, clique em lista suspensa de saudação e selecione Olá **leitura** permissão.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="8cfe6-133">Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8cfe6-134">Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="8cfe6-135">toocreate uma função de usuário analista de vendas dos EUA</span><span class="sxs-lookup"><span data-stu-id="8cfe6-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="8cfe6-136">No Gerenciador de Funções, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="8cfe6-137">Renomeie a função hello muito**analista de vendas dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="8cfe6-138">Dê a essa função a permissão **Leitura**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="8cfe6-139">Guia de filtros de linha hello e, em seguida, para Olá **DimGeography** tabela somente na coluna de filtro DAX hello, Olá tipo seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="8cfe6-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="8cfe6-140">Fórmula de um filtro de linha deve resolver tooa valor de booliano (verdadeiro/falso).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="8cfe6-141">Com essa fórmula, você está especificando que somente as linhas com valor de código de região de país do hello "US" estão visíveis toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="8cfe6-143">Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8cfe6-144">Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="8cfe6-145">toocreate uma função de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="8cfe6-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="8cfe6-146">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="8cfe6-147">Renomeie a função hello muito**administrador**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="8cfe6-148">Dê permissão de **Administrador** a essa função.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="8cfe6-149">Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8cfe6-150">Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="8cfe6-151">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="8cfe6-151">What's next?</span></span>
<span data-ttu-id="8cfe6-152">[Lição 12: Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
