---
title: Comece com uma amostra
description: "Power BI Embedded, use o SDK para adicionar relatórios interativos do Power BI a seu aplicativo de business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="71203-103">Introdução ao exemplo do Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71203-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="71203-104">Com o **Microsoft Power BI Embedded**, você pode integrar relatórios do Power BI diretamente a seus aplicativos móveis ou Web.</span><span class="sxs-lookup"><span data-stu-id="71203-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="71203-105">Neste artigo, apresentaremos a você o exemplo de introdução do **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="71203-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="71203-106">Antes de continuarmos, convém salvar os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="71203-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="71203-107">Eles o ajudarão ao integrar relatórios do Power BI ao aplicativo de exemplo e a seus próprios aplicativos também.</span><span class="sxs-lookup"><span data-stu-id="71203-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="71203-108">Exemplo de aplicativo Web do espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="71203-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="71203-109">Referência da API do Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71203-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="71203-110">[SDK do .NET do Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponível via NuGet)</span><span class="sxs-lookup"><span data-stu-id="71203-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="71203-111">Amostra inserida de relatório JavaScript</span><span class="sxs-lookup"><span data-stu-id="71203-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="71203-112">Antes que você possa configurar e executar o exemplo de introdução do Power BI Embedded, você precisa criar pelo menos uma **Coleção de Espaço de Trabalho** em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="71203-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="71203-113">Para aprender a criar um **Coleção de Espaço de Trabalho** no Portal do Azure, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="71203-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="71203-114">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="71203-114">Configure the sample app</span></span>

<span data-ttu-id="71203-115">Vamos orientar você sobre como configurar seu ambiente de desenvolvimento do Visual Studio para acessar os componentes necessários para executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="71203-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="71203-116">Baixe e descompacte a amostra [Power BI Embedded - Integrar um relatório em um aplicativo Web](http://go.microsoft.com/fwlink/?LinkId=761493) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="71203-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="71203-117">Abra **PowerBI-embedded.sln** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71203-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="71203-118">Talvez seja necessário executar o comando **Update-Package** no Console do Gerenciador de Pacotes do NuGET para atualizar os pacotes usados nesta solução.</span><span class="sxs-lookup"><span data-stu-id="71203-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="71203-119">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="71203-119">Build the solution.</span></span>
4. <span data-ttu-id="71203-120">Execute o aplicativo de console **ProvisionSample** .</span><span class="sxs-lookup"><span data-stu-id="71203-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="71203-121">No aplicativo de console de exemplo, você provisiona um espaço de trabalho e importa um arquivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="71203-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="71203-122">Para provisionar um novo **Espaço de trabalho**, selecione a opção 1, **Gerenciamento de coleção** e selecione a opção 6, **Provisionar um novo espaço de trabalho**</span><span class="sxs-lookup"><span data-stu-id="71203-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="71203-123">Para importar um novo **Relatório**, selecione a opção 2, **Gerenciamento de relatório** e selecione a opção 3, **Importar arquivo PBIX da Área de Trabalho em um espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="71203-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="71203-124">Insira o nome da sua **Coleção de Espaços de Trabalho** e a sua **Chave de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="71203-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="71203-125">Você pode obtê-los no **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="71203-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="71203-126">Para saber mais sobre como obter sua **Tecla de Acesso**, consulte [Exibir Chaves de Acesso de API do Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) na Introdução ao Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="71203-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="71203-127">Copie e salve a **ID do Espaço de Trabalho** recém-criada a usar posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="71203-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="71203-128">Depois que a **ID do Espaço de Trabalho** for criada, você poderá encontrá-la no **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="71203-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="71203-129">Para importar um arquivo PBIX para o **Espaço de Trabalho**, selecione a opção **6. Importe o arquivo da Área de Trabalho PBIX em um espaço de trabalho existente**.</span><span class="sxs-lookup"><span data-stu-id="71203-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="71203-130">Se você não tiver um arquivo PBIX prático, poderá baixar o [PBIX de Exemplo de Análise de Vendas](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="71203-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="71203-131">Se solicitado, insira um nome amigável para o **Conjunto de Dados**.</span><span class="sxs-lookup"><span data-stu-id="71203-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="71203-132">Você verá uma resposta semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="71203-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="71203-133">Se o arquivo PBIX contiver quaisquer conexões de consulta direta, execute a opção 7 para atualizar as cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="71203-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="71203-134">Neste ponto, um relatório PBIX do Power BI é importado para o seu **Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="71203-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="71203-135">Agora, vejamos como executar aplicativo Web de exemplo de introdução do **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="71203-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="71203-136">Executar o aplicativo Web de exemplo</span><span class="sxs-lookup"><span data-stu-id="71203-136">Run the sample web app</span></span>
<span data-ttu-id="71203-137">A amostra do aplicativo Web é um aplicativo de exemplo que renderiza relatórios importados para o seu **Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="71203-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="71203-138">Aqui está como configurar o aplicativo Web de exemplo.</span><span class="sxs-lookup"><span data-stu-id="71203-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="71203-139">Na solução **PowerBI-embedded** do Visual Studio, clique com o botão direito do mouse no aplicativo Web **EmbedSample** e escolha **Definir como projeto de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="71203-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="71203-140">Em **web.config**, no aplicativo Web **EmbedSample** edite o nome de **appSettings**: **AccessKey**, **WorkspaceCollection** e a **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="71203-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="71203-141">Execute o aplicativo Web **EmbedSample**.</span><span class="sxs-lookup"><span data-stu-id="71203-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="71203-142">Depois que você executar o aplicativo Web **EmbedSample**, o painel de navegação esquerdo deve conter um menu **Relatórios**.</span><span class="sxs-lookup"><span data-stu-id="71203-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="71203-143">Para exibir o relatório que você importou, expanda **Relatórios** e clique em um relatório.</span><span class="sxs-lookup"><span data-stu-id="71203-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="71203-144">Se você tivesse importado o [PBIX de Exemplo de Análise de Vendas](http://go.microsoft.com/fwlink/?LinkID=780547), o aplicativo Web de exemplo teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="71203-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="71203-145">Depois de clicar em um relatório, o aplicativo Web **EmbedSample** deve ter essa aparência:</span><span class="sxs-lookup"><span data-stu-id="71203-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="71203-146">Explorar o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="71203-146">Explore the sample code</span></span>

<span data-ttu-id="71203-147">A amostra do **Microsoft Power BI Embedded** é um aplicativo Web de exemplo que mostra como integrar relatórios do **Power BI** ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71203-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="71203-148">Ele usa um MVC (Model-View-Controller) para demonstrar as práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="71203-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="71203-149">Esta seção destaca as partes do código de exemplo que você pode explorar dentro da solução de aplicativo Web **PowerBI-embedded**.</span><span class="sxs-lookup"><span data-stu-id="71203-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="71203-150">O padrão Model-View-Controller (MVC) separa a modelagem de domínio, a apresentação e as ações com base na entrada do usuário em três classes separadas: Modelo, Exibição e Controle.</span><span class="sxs-lookup"><span data-stu-id="71203-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="71203-151">Para saber mais sobre o MVC, consulte [Aprenda sobre o ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="71203-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="71203-152">O código de exemplo do **Microsoft Power BI Embedded** é separado conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="71203-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="71203-153">Cada seção inclui o nome do arquivo na solução PowerBI-embedded.sln para que você possa localizar facilmente o código no exemplo.</span><span class="sxs-lookup"><span data-stu-id="71203-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="71203-154">Esta seção é um resumo do código de exemplo que mostra como o código foi escrito.</span><span class="sxs-lookup"><span data-stu-id="71203-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="71203-155">Para ver o exemplo completo, carregue a solução PowerBI-embedded.sln no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71203-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="71203-156">Modelo</span><span class="sxs-lookup"><span data-stu-id="71203-156">Model</span></span>

<span data-ttu-id="71203-157">O exemplo conta com um **ReportsViewModel** e um **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="71203-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="71203-158">**ReportsViewModel.cs**: representa relatórios do Power BI.</span><span class="sxs-lookup"><span data-stu-id="71203-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="71203-159">**ReportViewModel.cs**: representa um relatório do Power BI.</span><span class="sxs-lookup"><span data-stu-id="71203-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="71203-160">Cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="71203-160">Connection string</span></span>

<span data-ttu-id="71203-161">A cadeia de conexão deve estar no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="71203-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="71203-162">Usar atributos comuns de servidor e de banco de dados falhará.</span><span class="sxs-lookup"><span data-stu-id="71203-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="71203-163">Por exemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="71203-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="71203-164">Visualizar</span><span class="sxs-lookup"><span data-stu-id="71203-164">View</span></span>

<span data-ttu-id="71203-165">A **Exibição** gerencia a exibição de **Relatórios** do Power BI e de um **Relatório** do Power BI.</span><span class="sxs-lookup"><span data-stu-id="71203-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="71203-166">**Reports.cshtml**: faça a iteração de **Model.Reports** para criar um **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="71203-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="71203-167">O **ActionLink** é composto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="71203-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="71203-168">Parte</span><span class="sxs-lookup"><span data-stu-id="71203-168">Part</span></span> | <span data-ttu-id="71203-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="71203-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71203-170">Title</span><span class="sxs-lookup"><span data-stu-id="71203-170">Title</span></span> |<span data-ttu-id="71203-171">Nome do Relatório.</span><span class="sxs-lookup"><span data-stu-id="71203-171">Name of the Report.</span></span> |
| <span data-ttu-id="71203-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="71203-172">QueryString</span></span> |<span data-ttu-id="71203-173">Um link para a ID de Relatório.</span><span class="sxs-lookup"><span data-stu-id="71203-173">A link to the Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="71203-174">Report.cshtml: defina o **Model.AccessToken** e a expressão Lambda para **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="71203-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="71203-175">Controller</span><span class="sxs-lookup"><span data-stu-id="71203-175">Controller</span></span>

<span data-ttu-id="71203-176">**DashboardController.cs**: cria um PowerBIClient que passa um **token de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="71203-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="71203-177">Um JWT (Token Web JSON) é gerado da **Chave de Assinatura** para obter as **Credenciais**.</span><span class="sxs-lookup"><span data-stu-id="71203-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="71203-178">As **Credenciais** são usadas para criar uma instância de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="71203-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="71203-179">Quando tiver uma instância de **PowerBIClient**, você poderá chamar GetReports() e GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="71203-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="71203-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="71203-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="71203-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="71203-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="71203-182">Tarefa<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="71203-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="71203-183">Integrar um relatório em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="71203-183">Integrate a report into your app</span></span>

<span data-ttu-id="71203-184">Quando tiver um **Relatório**, você deverá usar um **IFrame** para inserir o **Relatório** do Power BI.</span><span class="sxs-lookup"><span data-stu-id="71203-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="71203-185">Veja um trecho de código do powerbi.js na amostra do **Microsoft Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="71203-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="71203-186">Filtrar relatórios inseridos no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="71203-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="71203-187">Você pode filtrar um relatório inserido usando uma sintaxe de URL.</span><span class="sxs-lookup"><span data-stu-id="71203-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="71203-188">Para fazer isso, adicione um parâmetro de cadeia de caracteres de consulta **$filter** com um operador **eq** à sua URL de origem do iFrame com o filtro especificado.</span><span class="sxs-lookup"><span data-stu-id="71203-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="71203-189">Aqui está a sintaxe de consulta de filtro:</span><span class="sxs-lookup"><span data-stu-id="71203-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="71203-190">{tableName/fieldName} não pode incluir espaços ou caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="71203-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="71203-191">O {fieldValue} aceita um único valor categórico.</span><span class="sxs-lookup"><span data-stu-id="71203-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="71203-192">Consulte também</span><span class="sxs-lookup"><span data-stu-id="71203-192">See also</span></span>

[<span data-ttu-id="71203-193">Cenários comuns do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71203-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="71203-194">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71203-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="71203-195">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="71203-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="71203-196">Criar um novo relatório de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="71203-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="71203-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="71203-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="71203-198">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="71203-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="71203-199">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="71203-199">More questions?</span></span> [<span data-ttu-id="71203-200">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="71203-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
