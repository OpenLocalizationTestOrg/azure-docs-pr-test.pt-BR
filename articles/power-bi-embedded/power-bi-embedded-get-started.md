---
title: "Introdução ao Microsoft Power BI Embedded"
description: "Power BI Embedded, adicione relatórios interativos do Power BI a seu aplicativo de business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="86ad4-103">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="86ad4-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="86ad4-104">**Power BI Embedded** é um serviço do Azure que permite que os desenvolvedores de aplicativos adicionem relatórios interativos do Power BI a seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="86ad4-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="86ad4-105">**Power BI Embedded** funciona com aplicativos existentes sem precisar reprojetar ou alterar os maneira como os usuários entram.</span><span class="sxs-lookup"><span data-stu-id="86ad4-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="86ad4-106">Os recursos para o **Microsoft Power BI Embedded** são provisionados por meio de [APIs do ARM do Azure](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="86ad4-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="86ad4-107">Nesse caso, o recurso que você provisiona é uma **Coleção de Espaços de Trabalho do Power BI**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="86ad4-108">Criar uma coleção de espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="86ad4-108">Create a workspace collection</span></span>

<span data-ttu-id="86ad4-109">Uma **coleção de espaços de trabalho** é o recurso mais avançado do Azure e um contêiner para o conteúdo que será inserido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86ad4-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="86ad4-110">Uma **Coleção de espaços de trabalho** pode ser criada de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="86ad4-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="86ad4-111">Usando o Portal do Azure manualmente</span><span class="sxs-lookup"><span data-stu-id="86ad4-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="86ad4-112">Programaticamente, usando as APIs do ARM (Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="86ad4-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="86ad4-113">Vamos percorrer as etapas para criar uma **Coleção de espaços de trabalho** usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86ad4-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="86ad4-114">Abra e entre no **Portal do Azure**: [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86ad4-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="86ad4-115">Clique em **+ Novo** no painel superior.</span><span class="sxs-lookup"><span data-stu-id="86ad4-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="86ad4-116">Em **Dados + Análise**, clique em **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="86ad4-117">Na **Folha da Coleção de Espaços de Trabalho**, insira as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="86ad4-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="86ad4-118">Para ver **Preços**, confira [Preço do Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="86ad4-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="86ad4-119">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-119">Click **Create**.</span></span>

<span data-ttu-id="86ad4-120">A **Coleção de espaços de trabalho** levará alguns minutos para provisionar.</span><span class="sxs-lookup"><span data-stu-id="86ad4-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="86ad4-121">Quando ela for concluída, você será levado para a **Folha de Coleção de espaços de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="86ad4-122">A **Folha de Criação** contém as informações necessárias para chamar as APIs que criam espaços de trabalho e implanta conteúdo nelas.</span><span class="sxs-lookup"><span data-stu-id="86ad4-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="86ad4-123">Exibir chaves de acesso da API do Power BI</span><span class="sxs-lookup"><span data-stu-id="86ad4-123">View Power BI API access keys</span></span>

<span data-ttu-id="86ad4-124">Uma das informações mais importantes necessárias para chamar as APIs REST do Power BI são as **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="86ad4-125">Elas são usadas para gerar os **tokens do aplicativo** que são usados na autenticação das solicitações de API.</span><span class="sxs-lookup"><span data-stu-id="86ad4-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="86ad4-126">Para exibir suas **Chaves de Acesso**, clique em **Chaves de Acesso** na **Folha de Configurações**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="86ad4-127">Para saber mais sobre **tokens de aplicativo**, confira [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="86ad4-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="86ad4-128">Você notará que tem duas chaves.</span><span class="sxs-lookup"><span data-stu-id="86ad4-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="86ad4-129">Copie essas chaves e armazene-as com segurança em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86ad4-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="86ad4-130">É muito importante tratar essas chaves como faria com uma senha, pois elas darão acesso a todo o conteúdo em sua **Coleção de espaços de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="86ad4-131">Embora duas chaves estejam listadas, somente uma chave é usada de cada vez.</span><span class="sxs-lookup"><span data-stu-id="86ad4-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="86ad4-132">A segunda chave é fornecida para regenerar as chaves periodicamente sem interromper o acesso ao serviço.</span><span class="sxs-lookup"><span data-stu-id="86ad4-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="86ad4-133">Agora que você tem uma instância do Power BI para seu aplicativo e as **Chaves de Acesso**, pode importar um relatório em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86ad4-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="86ad4-134">Antes de aprender como importar um relatório, a próxima seção descreve a criação de relatórios e conjuntos de dados do Power BI para inserir em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86ad4-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="86ad4-135">Trabalhando com espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="86ad4-135">Working with workspaces</span></span>

<span data-ttu-id="86ad4-136">Depois que você criou sua coleção de espaço de trabalho, você precisará criar um espaço de trabalho que conterá seus relatórios e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="86ad4-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="86ad4-137">Para criar um espaço de trabalho, você precisará usar o [API de REST do espaço de trabalho de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="86ad4-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="86ad4-138">Criar relatórios e conjuntos de dados do Power BI para inserir em um aplicativo usando o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="86ad4-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="86ad4-139">Agora que você criou uma instância do Power BI para seu aplicativo e tem **Chaves de Acesso**, precisa criar os relatórios e conjuntos de dados do Power BI que deseja inserir.</span><span class="sxs-lookup"><span data-stu-id="86ad4-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="86ad4-140">Conjuntos de dados e relatórios podem ser criados usando o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="86ad4-141">Você pode baixar o [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="86ad4-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="86ad4-142">Ou, para começar rapidamente, você pode baixar o [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)(PBIX de exemplo de análise de varejo).</span><span class="sxs-lookup"><span data-stu-id="86ad4-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="86ad4-143">Para saber mais sobre como usar o **Power BI Desktop**, confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="86ad4-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="86ad4-144">Com o **Power BI Desktop**, você se conecta à fonte de dados importando uma cópia dos dados para o **Power BI Desktop** ou se conectando diretamente à fonte de dados usando o **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="86ad4-145">Estas são as diferenças entre o uso de **Importar** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="86ad4-146">Importar</span><span class="sxs-lookup"><span data-stu-id="86ad4-146">Import</span></span> | <span data-ttu-id="86ad4-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="86ad4-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="86ad4-148">Tabelas, colunas, *e dados* são importados ou copiados para o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="86ad4-149">Ao trabalhar com visualizações, o **Power BI Desktop** consulta uma cópia dos dados.</span><span class="sxs-lookup"><span data-stu-id="86ad4-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="86ad4-150">Para ver as alterações ocorridas nos dados subjacentes, você deve atualizar ou importar novamente um conjunto de dados completo e atual.</span><span class="sxs-lookup"><span data-stu-id="86ad4-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="86ad4-151">Somente *tabelas e colunas* são importadas ou copiadas para o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="86ad4-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="86ad4-152">Ao trabalhar com as visualizações, o **Power BI Desktop** consulta a fonte de dados subjacente, o que significa que você sempre estará exibindo os dados atuais.</span><span class="sxs-lookup"><span data-stu-id="86ad4-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="86ad4-153">Para saber mais sobre como se conectar a uma fonte de dados, confira [Conectar-se a uma fonte de dados](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="86ad4-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="86ad4-154">Depois de salvar seu trabalho no **Power BI Desktop**, um arquivo PBIX será criado.</span><span class="sxs-lookup"><span data-stu-id="86ad4-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="86ad4-155">Esse arquivo contém o relatório.</span><span class="sxs-lookup"><span data-stu-id="86ad4-155">This file contains your report.</span></span> <span data-ttu-id="86ad4-156">Além disso, se você importar dados, o PBIX conterá o conjunto de dados completo, mas se usar o **DirectQuery**, o PBIX conterá apenas um esquema de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="86ad4-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="86ad4-157">Implante o PBIX em seu espaço de trabalho programaticamente usando a [API de importação do Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="86ad4-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="86ad4-158">**Power BI Embedded** tem APIs adicionais para alterar o servidor e o banco de dados para onde seu conjunto de dados está apontando e para definir uma credencial da conta de serviço que o conjunto de dados usará a fim de se conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="86ad4-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="86ad4-159">Confira [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) e [Correção de fonte de dados do gateway](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="86ad4-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="86ad4-160">Criar relatórios e conjuntos de dados do Power BI usando APIs</span><span class="sxs-lookup"><span data-stu-id="86ad4-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="86ad4-161">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="86ad4-161">Datsets</span></span>

<span data-ttu-id="86ad4-162">Você pode criar conjuntos de dados no Power BI Embedded usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="86ad4-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="86ad4-163">Em seguida, você pode enviar dados por push para seu conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="86ad4-163">You can then push data into your dataset.</span></span> <span data-ttu-id="86ad4-164">Isso permite que você trabalhe com dados sem a necessidade do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="86ad4-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="86ad4-165">Para saber mais, veja [Postar conjuntos de dados](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="86ad4-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="86ad4-166">Relatórios</span><span class="sxs-lookup"><span data-stu-id="86ad4-166">Reports</span></span>

<span data-ttu-id="86ad4-167">Você pode criar um relatório de um conjunto de dados diretamente em seu aplicativo usando a API de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="86ad4-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="86ad4-168">Para saber mais, veja [Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="86ad4-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="86ad4-169">Consulte também</span><span class="sxs-lookup"><span data-stu-id="86ad4-169">See Also</span></span>

[<span data-ttu-id="86ad4-170">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="86ad4-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="86ad4-171">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="86ad4-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="86ad4-172">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="86ad4-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="86ad4-173">[Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Salvar relatórios](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="86ad4-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="86ad4-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="86ad4-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="86ad4-175">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="86ad4-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="86ad4-176">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="86ad4-176">More questions?</span></span> [<span data-ttu-id="86ad4-177">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="86ad4-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)

