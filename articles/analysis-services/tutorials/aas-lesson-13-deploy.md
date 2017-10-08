---
<span data-ttu-id="fae1e-101">título: aaa "lição do tutorial do Azure Analysis Services 13: implantar | Descrição de Microsoft Docs": descreve como o tutorial de saudação toodeploy projeto tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="fae1e-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="fae1e-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="fae1e-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="fae1e-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 17/07/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="fae1e-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="fae1e-104">Lição 13: implantar</span><span class="sxs-lookup"><span data-stu-id="fae1e-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="fae1e-105">Nesta lição, você configurar propriedades de implantação. especificando um tooand de toodeploy de servidor um nome para o modelo de saudação do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="fae1e-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="fae1e-106">Em seguida, implantar toothat instância de modelo a saudação.</span><span class="sxs-lookup"><span data-stu-id="fae1e-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="fae1e-107">Depois que o modelo é implantado, os usuários podem se conectar tooit usando um aplicativo cliente de relatório.</span><span class="sxs-lookup"><span data-stu-id="fae1e-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="fae1e-108">mais, consulte toolearn [implantar serviços de análise de tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="fae1e-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="fae1e-109">Estimado tempo toocomplete nesta lição: **5 minutos**</span><span class="sxs-lookup"><span data-stu-id="fae1e-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="fae1e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fae1e-110">Prerequisites</span></span>  
<span data-ttu-id="fae1e-111">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="fae1e-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="fae1e-112">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 12: analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="fae1e-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="fae1e-113">Você deve ter [permissões de administrador](../analysis-services-server-admins.md) em Olá remoto do Analysis Services server em ordem toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="fae1e-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="fae1e-114">Se você instalou o banco de dados de exemplo hello AdventureWorksDW2014 em um SQL Server local e você estiver implantando o servidor do modelo tooan Azure Analysis Services, uma [gateway de dados no local](../analysis-services-gateway.md) é necessária.</span><span class="sxs-lookup"><span data-stu-id="fae1e-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="fae1e-115">Implantar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="fae1e-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="fae1e-116">Propriedades de implantação tooconfigure</span><span class="sxs-lookup"><span data-stu-id="fae1e-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="fae1e-117">Em **Gerenciador de soluções**, Olá atalho **de vendas pela Internet AW** do projeto e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="fae1e-118">Em Olá **páginas de propriedades de vendas de Internet AW** caixa de diálogo **servidor de implantação**, em Olá **Server** propriedade, digite servidor completo hello.</span><span class="sxs-lookup"><span data-stu-id="fae1e-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="fae1e-120">Em Olá **banco de dados** propriedade, digite **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="fae1e-121">Em Olá **nome do modelo** propriedade, digite **modelo de vendas do Adventure Works Internet**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="fae1e-122">Verifique suas seleções e então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="fae1e-123">Olá toodeploy Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="fae1e-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="fae1e-124">Em **Solution Explorer**, Olá do botão direito do mouse **de vendas pela Internet AW** projeto > **criar**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="fae1e-125">Saudação de atalho **de vendas pela Internet AW** projeto > **implantar**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="fae1e-126">Ao implantar tooAzure Analysis Services, você pode ser solicitado tooenter sua conta.</span><span class="sxs-lookup"><span data-stu-id="fae1e-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="fae1e-127">Insira sua conta e senha organizacionais, por exemplo, nancy@adventureworks.com. Essa conta deve estar em Administradores no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="fae1e-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="fae1e-128">caixa de diálogo implantar Olá aparece e exibe o status de implantação de saudação de saudação metadados e cada tabela incluído no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fae1e-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="fae1e-130">Quando a implantação for concluída com êxito, vá em frente e clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="fae1e-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="fae1e-131">Conclusão</span><span class="sxs-lookup"><span data-stu-id="fae1e-131">Conclusion</span></span>  
<span data-ttu-id="fae1e-132">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="fae1e-132">Congratulations!</span></span> <span data-ttu-id="fae1e-133">Você terminou de criar e implantar seu primeiro modelo tabular do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="fae1e-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="fae1e-134">Este tutorial ajudou você a concluir as tarefas mais comuns de saudação na criação de um modelo de tabela.</span><span class="sxs-lookup"><span data-stu-id="fae1e-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="fae1e-135">Agora que o modelo do Adventure Works Internet Sales é implantado, você pode usar o modelo de saudação do SQL Server Management Studio toomanage; crie scripts de processo e um plano de backup.</span><span class="sxs-lookup"><span data-stu-id="fae1e-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="fae1e-136">Os usuários agora também podem se conectar toohello modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou Power BI.</span><span class="sxs-lookup"><span data-stu-id="fae1e-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="fae1e-138">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="fae1e-138">What's next?</span></span>
<span data-ttu-id="fae1e-139">[Conecte-se com o Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="fae1e-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="fae1e-140">[Lição suplementar - Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="fae1e-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="fae1e-141">[Lição suplementar - Linhas de detalhes](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="fae1e-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="fae1e-142">Lição Suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="fae1e-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
