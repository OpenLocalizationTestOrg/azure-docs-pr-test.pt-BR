---
title: "aaaGet com um exemplo de Introdução"
description: "Power BI inserido, use o SDK tooadd relatórios interativos do Power BI em seu aplicativo de business intelligence"
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
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="51748-103">Introdução ao exemplo do Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51748-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="51748-104">Com o **Microsoft Power BI Embedded**, você pode integrar relatórios do Power BI diretamente a seus aplicativos móveis ou Web.</span><span class="sxs-lookup"><span data-stu-id="51748-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="51748-105">Neste artigo, apresentaremos toohello **Power BI inserido** exemplo de Introdução get.</span><span class="sxs-lookup"><span data-stu-id="51748-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="51748-106">Antes de continuarmos, você provavelmente vai querer Olá toosave recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="51748-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="51748-107">Eles ajudá-lo ao integrar relatórios do Power BI em um aplicativo de exemplo hello e seus próprios aplicativos muito.</span><span class="sxs-lookup"><span data-stu-id="51748-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="51748-108">Exemplo de aplicativo Web do espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="51748-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="51748-109">Referência da API do Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51748-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="51748-110">[SDK do .NET do Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponível via NuGet)</span><span class="sxs-lookup"><span data-stu-id="51748-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="51748-111">Amostra inserida de relatório JavaScript</span><span class="sxs-lookup"><span data-stu-id="51748-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="51748-112">Antes de você pode configurar e exemplo de Introdução ao executar Olá obter Power BI inserido, você precisa toocreate pelo menos um **coleta de espaço de trabalho** na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51748-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="51748-113">toolearn como toocreate uma **coleta de espaço de trabalho** em Olá Portal do Azure, consulte [guia de Introdução ao Power BI inserido](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51748-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="51748-114">Configurar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="51748-114">Configure hello sample app</span></span>

<span data-ttu-id="51748-115">Vamos examinar a configuração de seu aplicativo de exemplo Visual Studio desenvolvimento ambiente tooaccess Olá componentes necessários toorun hello.</span><span class="sxs-lookup"><span data-stu-id="51748-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="51748-116">Baixe e descompacte Olá [Power BI inserido - integrar um relatório em um aplicativo web](http://go.microsoft.com/fwlink/?LinkId=761493) exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="51748-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="51748-117">Abra **PowerBI-embedded.sln** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51748-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="51748-118">Talvez seja necessário Olá tooexecute **pacote de atualização** do hello Console de Gerenciador de pacote do NuGET em ordem tooupdate Olá pacotes usados nesta solução.</span><span class="sxs-lookup"><span data-stu-id="51748-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="51748-119">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="51748-119">Build hello solution.</span></span>
4. <span data-ttu-id="51748-120">Executar Olá **ProvisionSample** aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="51748-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="51748-121">No aplicativo de console do exemplo hello, você provisiona um espaço de trabalho e importa um arquivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="51748-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="51748-122">tooprovision um novo **espaço de trabalho**, selecione a opção 1, **gerenciamento coleção**e, em seguida, selecione a opção 6, **provisionar um novo espaço de trabalho**</span><span class="sxs-lookup"><span data-stu-id="51748-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="51748-123">tooimport um novo **relatório**, selecione a opção 2, **relatório gerenciamento**e, em seguida, selecione a opção 3, **arquivo de importação PBIX Desktop em um espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="51748-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="51748-124">Insira o nome da sua **Coleção de Espaços de Trabalho** e a sua **Chave de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="51748-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="51748-125">Você pode obter em Olá **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="51748-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="51748-126">toolearn mais informações sobre como tooget o **chave de acesso**, consulte [chaves de acesso de API do modo de exibição Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) na introdução ao Microsoft Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="51748-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="51748-127">Copie e salve Olá recém-criado **ID do espaço de trabalho** toouse neste artigo.</span><span class="sxs-lookup"><span data-stu-id="51748-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="51748-128">Depois de saudação **ID do espaço de trabalho** é criado, você pode encontrar hello **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="51748-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="51748-129">o arquivo de tooimport um PBIX em seu **espaço de trabalho**, selecione a opção **6. Importe o arquivo da Área de Trabalho PBIX em um espaço de trabalho existente**.</span><span class="sxs-lookup"><span data-stu-id="51748-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="51748-130">Se você não tiver um PBIX útil do arquivo, você pode baixar Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="51748-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="51748-131">Se solicitado, insira um nome amigável para o **Conjunto de Dados**.</span><span class="sxs-lookup"><span data-stu-id="51748-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="51748-132">Você verá uma resposta semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="51748-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="51748-133">Se o arquivo PBIX contiver quaisquer conexões de consulta direta, execute cadeias de caracteres da conexão Olá opção tooupdate 7.</span><span class="sxs-lookup"><span data-stu-id="51748-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="51748-134">Neste ponto, um relatório PBIX do Power BI é importado para o seu **Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="51748-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="51748-135">Agora, vamos dar uma olhada em como Olá toorun **Power BI inserido** obter o aplicativo web de exemplo de Introdução.</span><span class="sxs-lookup"><span data-stu-id="51748-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="51748-136">Execute o aplicativo de web de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="51748-136">Run hello sample web app</span></span>
<span data-ttu-id="51748-137">Olá aplicativo web de exemplo é um aplicativo de exemplo que renderiza relatórios importados para o **espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="51748-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="51748-138">Aqui está como tooconfigure Olá aplicativo web de exemplo.</span><span class="sxs-lookup"><span data-stu-id="51748-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="51748-139">Em Olá **inserido PowerBI** solução do Visual Studio, direito clique Olá **EmbedSample** aplicativo web e escolha **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="51748-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="51748-140">Em **Web. config**, em Olá **EmbedSample** aplicativo web, edite Olá **appSettings**: **AccessKey**,  **WorkspaceCollection** nome, e **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="51748-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="51748-141">Executar Olá **EmbedSample** aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="51748-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="51748-142">Quando você executar Olá **EmbedSample** aplicativo web, o painel de navegação esquerdo Olá deve conter um **relatórios** menu.</span><span class="sxs-lookup"><span data-stu-id="51748-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="51748-143">relatório de saudação tooview você importou, expanda **relatórios**e clique em um relatório.</span><span class="sxs-lookup"><span data-stu-id="51748-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="51748-144">Se você importou Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547), aplicativo de web de exemplo hello teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="51748-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="51748-145">Depois de clicar em um relatório, Olá **EmbedSample** aplicativo web deve ser algo isso:</span><span class="sxs-lookup"><span data-stu-id="51748-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="51748-146">Explorar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="51748-146">Explore hello sample code</span></span>

<span data-ttu-id="51748-147">Olá **Microsoft Power BI inserido** exemplo é um aplicativo da web de exemplo que mostra como toointegrate **Power BI** relatórios em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51748-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="51748-148">Ele usa um Model-View-Controller (MVC) práticas recomendadas de toodemonstrate de padrão de design.</span><span class="sxs-lookup"><span data-stu-id="51748-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="51748-149">Esta seção destaca as partes do código de exemplo hello que você pode explorar em hello **inserido PowerBI** solução de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="51748-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="51748-150">Olá, o padrão Model-View-Controller (MVC) separa modelagem de saudação do domínio hello, apresentação hello e as ações de saudação com base na entrada do usuário em três classes separadas: modelo, exibição e controle.</span><span class="sxs-lookup"><span data-stu-id="51748-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="51748-151">toolearn mais sobre o MVC, consulte [Saiba mais sobre ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="51748-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="51748-152">Olá **Microsoft Power BI inserido** código de exemplo é separado da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="51748-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="51748-153">Cada seção inclui o nome do arquivo hello no hello PowerBI embedded.sln solução para que você pode localizar facilmente código Olá no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="51748-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="51748-154">Esta seção é um resumo Olá códigos de exemplo que mostra como o código de saudação foi escrito.</span><span class="sxs-lookup"><span data-stu-id="51748-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="51748-155">saudação de tooview completa de exemplo, carregue a solução Olá PowerBI embedded.sln no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51748-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="51748-156">Modelo</span><span class="sxs-lookup"><span data-stu-id="51748-156">Model</span></span>

<span data-ttu-id="51748-157">exemplo Hello tem um **ReportsViewModel** e **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="51748-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="51748-158">**ReportsViewModel.cs**: representa relatórios do Power BI.</span><span class="sxs-lookup"><span data-stu-id="51748-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="51748-159">**ReportViewModel.cs**: representa um relatório do Power BI.</span><span class="sxs-lookup"><span data-stu-id="51748-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="51748-160">Cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="51748-160">Connection string</span></span>

<span data-ttu-id="51748-161">cadeia de caracteres de conexão Olá deve ser Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="51748-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="51748-162">Usar atributos comuns de servidor e de banco de dados falhará.</span><span class="sxs-lookup"><span data-stu-id="51748-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="51748-163">Por exemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="51748-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="51748-164">Visualizar</span><span class="sxs-lookup"><span data-stu-id="51748-164">View</span></span>

<span data-ttu-id="51748-165">Olá **exibição** gerencia a exibição de saudação do Power BI **relatórios** e um Power BI **relatório**.</span><span class="sxs-lookup"><span data-stu-id="51748-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="51748-166">**Reports.cshtml**: iterar **Model.Reports** toocreate um **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="51748-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="51748-167">Olá **ActionLink** é composto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="51748-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="51748-168">Parte</span><span class="sxs-lookup"><span data-stu-id="51748-168">Part</span></span> | <span data-ttu-id="51748-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="51748-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51748-170">Title</span><span class="sxs-lookup"><span data-stu-id="51748-170">Title</span></span> |<span data-ttu-id="51748-171">Nome do relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="51748-171">Name of hello Report.</span></span> |
| <span data-ttu-id="51748-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="51748-172">QueryString</span></span> |<span data-ttu-id="51748-173">Um link de toohello ID do relatório.</span><span class="sxs-lookup"><span data-stu-id="51748-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="51748-174">Report.cshtml: Definir Olá **Model.AccessToken**, e Olá expressão Lambda para **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="51748-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="51748-175">Controller</span><span class="sxs-lookup"><span data-stu-id="51748-175">Controller</span></span>

<span data-ttu-id="51748-176">**DashboardController.cs**: cria um PowerBIClient que passa um **token de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="51748-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="51748-177">Um JSON Web Token (JWT) é gerada a partir Olá **chave de assinatura** tooget Olá **credenciais**.</span><span class="sxs-lookup"><span data-stu-id="51748-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="51748-178">Olá **credenciais** é usada toocreate uma instância de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="51748-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="51748-179">Quando tiver uma instância de **PowerBIClient**, você poderá chamar GetReports() e GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="51748-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="51748-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="51748-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="51748-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="51748-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="51748-182">Tarefa<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="51748-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="51748-183">Integrar um relatório em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="51748-183">Integrate a report into your app</span></span>

<span data-ttu-id="51748-184">Depois que você tiver um **relatório**, você usa um **IFrame** tooembed Olá Power BI **relatório**.</span><span class="sxs-lookup"><span data-stu-id="51748-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="51748-185">Aqui está um trecho de código do powerbi.js no hello **Microsoft Power BI inserido** exemplo.</span><span class="sxs-lookup"><span data-stu-id="51748-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="51748-186">Filtrar relatórios inseridos no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="51748-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="51748-187">Você pode filtrar um relatório inserido usando uma sintaxe de URL.</span><span class="sxs-lookup"><span data-stu-id="51748-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="51748-188">toodo isso, você adiciona um **$filter** consultar o parâmetro de cadeia de caracteres com um **eq** operador tooyour iFrame src url com hello filtro especificado.</span><span class="sxs-lookup"><span data-stu-id="51748-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="51748-189">Aqui está a sintaxe de consulta de filtro hello:</span><span class="sxs-lookup"><span data-stu-id="51748-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="51748-190">{tableName/fieldName} não pode incluir espaços ou caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="51748-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="51748-191">Olá {fieldValue} aceita um único valor categórico.</span><span class="sxs-lookup"><span data-stu-id="51748-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="51748-192">Consulte também</span><span class="sxs-lookup"><span data-stu-id="51748-192">See also</span></span>

[<span data-ttu-id="51748-193">Cenários comuns do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51748-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="51748-194">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51748-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="51748-195">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="51748-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="51748-196">Criar um novo relatório de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="51748-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="51748-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="51748-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="51748-198">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="51748-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="51748-199">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="51748-199">More questions?</span></span> [<span data-ttu-id="51748-200">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="51748-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
