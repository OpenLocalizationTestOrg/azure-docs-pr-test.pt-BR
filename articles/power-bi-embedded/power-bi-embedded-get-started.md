---
title: aaaGet iniciado com o Microsoft Power BI Embedded
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
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="c50a3-103">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c50a3-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="c50a3-104">**Power BI inserido** é um serviço do Azure que tooadd de desenvolvedores de aplicativos permite que relatórios interativos do Power BI em seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c50a3-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="c50a3-105">**Power BI inserido** funciona com aplicativos existentes sem necessidade reestruturação ou alterar a maneira como os usuários-Olá entrar.</span><span class="sxs-lookup"><span data-stu-id="c50a3-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="c50a3-106">Recursos para **Microsoft Power BI inserido** provisionados usando Olá [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="c50a3-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="c50a3-107">Nesse caso, o recurso de saudação provisionar é um **coleta de espaço de trabalho do Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="c50a3-108">Criar uma coleção de espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="c50a3-108">Create a workspace collection</span></span>

<span data-ttu-id="c50a3-109">Um **coleta de espaço de trabalho** é o recurso do Azure do nível superior hello e um contêiner para conteúdo de saudação que será inserido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c50a3-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="c50a3-110">Uma **Coleção de espaços de trabalho** pode ser criada de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="c50a3-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="c50a3-111">Manualmente usando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c50a3-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="c50a3-112">Programaticamente, usando Olá APIs de Manager(ARM) de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c50a3-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="c50a3-113">Vamos percorrer Olá etapas toobuild um **coleta de espaço de trabalho** usando Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50a3-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="c50a3-114">Abra e entre no **Portal do Azure**: [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c50a3-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="c50a3-115">Clique em **+ novo** no painel superior hello.</span><span class="sxs-lookup"><span data-stu-id="c50a3-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="c50a3-116">Em **Dados + Análise**, clique em **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="c50a3-117">Em Olá **folha de coleta de espaço de trabalho**, insira informações Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="c50a3-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="c50a3-118">Para ver **Preços**, confira [Preço do Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="c50a3-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="c50a3-119">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-119">Click **Create**.</span></span>

<span data-ttu-id="c50a3-120">Olá **coleta de espaço de trabalho** levará tooprovision de alguns instantes.</span><span class="sxs-lookup"><span data-stu-id="c50a3-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="c50a3-121">Quando concluído, você será levado toohello **folha de coleta de espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="c50a3-122">Olá **criação folha** contém informações de saudação necessárias toocall Olá APIs que criar espaços de trabalho e implantar conteúdo toothem.</span><span class="sxs-lookup"><span data-stu-id="c50a3-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="c50a3-123">Exibir chaves de acesso da API do Power BI</span><span class="sxs-lookup"><span data-stu-id="c50a3-123">View Power BI API access keys</span></span>

<span data-ttu-id="c50a3-124">Um dos mais importantes de partes de informações necessárias toocall Olá APIs REST do Power BI de saudação são Olá **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="c50a3-125">Estes são usados toogenerate Olá **tokens do aplicativo** que são usada tooauthenticate suas solicitações de API.</span><span class="sxs-lookup"><span data-stu-id="c50a3-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="c50a3-126">tooview seu **chaves de acesso**, clique em **chaves de acesso** em Olá **folha configurações**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="c50a3-127">Para saber mais sobre **tokens de aplicativo**, confira [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="c50a3-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="c50a3-128">Você notará que tem duas chaves.</span><span class="sxs-lookup"><span data-stu-id="c50a3-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="c50a3-129">Copie essas chaves e armazene-as com segurança em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c50a3-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="c50a3-130">É muito importante tratar essas chaves como você faria com uma senha, pois será fornecem acesso tooall Olá conteúdo no seu **coleta de espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="c50a3-131">Embora duas chaves estejam listadas, somente uma chave é usada de cada vez.</span><span class="sxs-lookup"><span data-stu-id="c50a3-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="c50a3-132">segunda chave de saudação é fornecido para que você periodicamente pode regenerar chaves sem interromper o serviço de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="c50a3-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="c50a3-133">Agora que você tem uma instância do Power BI para seu aplicativo e as **Chaves de Acesso**, pode importar um relatório em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c50a3-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="c50a3-134">Antes, você aprenderá como tooimport um relatório, a próxima seção de saudação descreve criando tooembed de conjuntos de dados e relatórios do Power BI em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c50a3-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="c50a3-135">Trabalhando com espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="c50a3-135">Working with workspaces</span></span>

<span data-ttu-id="c50a3-136">Depois de criar sua coleção do espaço de trabalho, você precisará toocreate um espaço de trabalho que conterá os relatórios e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="c50a3-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="c50a3-137">toocreate um espaço de trabalho, você precisará Olá toouse [API de REST do espaço de trabalho de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="c50a3-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="c50a3-138">Criar tooembed de conjuntos de dados e relatórios do Power BI em um aplicativo usando o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c50a3-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="c50a3-139">Agora que você criou uma instância do Power BI para seu aplicativo e ter **chaves de acesso**, você precisará toocreate Olá Power BI conjuntos de dados e relatórios que você deseja tooembed.</span><span class="sxs-lookup"><span data-stu-id="c50a3-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="c50a3-140">Conjuntos de dados e relatórios podem ser criados usando o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="c50a3-141">Você pode baixar o [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="c50a3-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="c50a3-142">Ou, tooquickly começar, você pode baixar Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="c50a3-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="c50a3-143">toolearn mais informações sobre como toouse **Power BI Desktop**, consulte [guia de Introdução ao Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="c50a3-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="c50a3-144">Com **Power BI Desktop**, você se conectar tooyour fonte de dados importando uma cópia dos dados de saudação em **Power BI Desktop** ou conectar-se diretamente dados toohello fonte usando **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="c50a3-145">Aqui estão Olá diferenças entre usar **importação** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="c50a3-146">Importar</span><span class="sxs-lookup"><span data-stu-id="c50a3-146">Import</span></span> | <span data-ttu-id="c50a3-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="c50a3-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="c50a3-148">Tabelas, colunas, *e dados* são importados ou copiados para o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="c50a3-149">Ao trabalhar com visualizações, **Power BI Desktop** consultas uma cópia dos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c50a3-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="c50a3-150">toosee todas as alterações de dados subjacente toohello ocorreu, você deve atualizar ou importar novamente um dataset completo e atual.</span><span class="sxs-lookup"><span data-stu-id="c50a3-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="c50a3-151">Somente *tabelas e colunas* são importadas ou copiadas para o **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="c50a3-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="c50a3-152">Ao trabalhar com visualizações, **Power BI Desktop** consultas Olá a fonte de dados subjacente, que significa que você sempre está exibindo dados atuais.</span><span class="sxs-lookup"><span data-stu-id="c50a3-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="c50a3-153">Para obter mais informações sobre a fonte de dados tooa conexão, consulte [conectar fonte de dados de tooa](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="c50a3-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="c50a3-154">Depois de salvar seu trabalho no **Power BI Desktop**, um arquivo PBIX será criado.</span><span class="sxs-lookup"><span data-stu-id="c50a3-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="c50a3-155">Esse arquivo contém o relatório.</span><span class="sxs-lookup"><span data-stu-id="c50a3-155">This file contains your report.</span></span> <span data-ttu-id="c50a3-156">Além disso, se você importar Olá dados PBIX contém Olá conjunto de dados completo, ou se você usar **DirectQuery**, Olá PBIX contém apenas um esquema de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c50a3-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="c50a3-157">Implantar programaticamente Olá PBIX no espaço de trabalho usando Olá [API do Power BI importar](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="c50a3-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c50a3-158">**Power BI inserido** tem adicionais APIs toochange saudação do servidor e banco de dados que o conjunto de dados está apontando conjunto tooand uma credencial de conta de serviço que Olá conjunto de dados usará o banco de dados do tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c50a3-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="c50a3-159">Confira [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) e [Correção de fonte de dados do gateway](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="c50a3-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="c50a3-160">Criar relatórios e conjuntos de dados do Power BI usando APIs</span><span class="sxs-lookup"><span data-stu-id="c50a3-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="c50a3-161">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="c50a3-161">Datsets</span></span>

<span data-ttu-id="c50a3-162">Você pode criar conjuntos de dados no Power BI inserido usando Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="c50a3-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="c50a3-163">Em seguida, você pode enviar dados por push para seu conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c50a3-163">You can then push data into your dataset.</span></span> <span data-ttu-id="c50a3-164">Isso permite que você toowork com dados sem a necessidade de saudação do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c50a3-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="c50a3-165">Para saber mais, veja [Postar conjuntos de dados](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="c50a3-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="c50a3-166">Relatórios</span><span class="sxs-lookup"><span data-stu-id="c50a3-166">Reports</span></span>

<span data-ttu-id="c50a3-167">Você pode criar um relatório de um conjunto de dados diretamente em seu aplicativo usando Olá API JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c50a3-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="c50a3-168">Para saber mais, veja [Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="c50a3-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c50a3-169">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c50a3-169">See Also</span></span>

[<span data-ttu-id="c50a3-170">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="c50a3-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="c50a3-171">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c50a3-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="c50a3-172">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="c50a3-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="c50a3-173">[Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Salvar relatórios](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="c50a3-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="c50a3-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c50a3-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="c50a3-175">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="c50a3-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="c50a3-176">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="c50a3-176">More questions?</span></span> [<span data-ttu-id="c50a3-177">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="c50a3-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

