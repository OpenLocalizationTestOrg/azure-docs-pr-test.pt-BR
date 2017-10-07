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
# <a name="get-started-with-power-bi-embedded-sample"></a>Introdução ao exemplo do Power BI Embedded

Com o **Microsoft Power BI Embedded**, você pode integrar relatórios do Power BI diretamente a seus aplicativos móveis ou Web. Neste artigo, apresentaremos toohello **Power BI inserido** exemplo de Introdução get.

Antes de continuarmos, você provavelmente vai querer Olá toosave recursos a seguir. Eles ajudá-lo ao integrar relatórios do Power BI em um aplicativo de exemplo hello e seus próprios aplicativos muito.

* [Exemplo de aplicativo Web do espaço de trabalho](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Referência da API do Power BI Embedded](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [SDK do .NET do Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponível via NuGet)
* [Amostra inserida de relatório JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Antes de você pode configurar e exemplo de Introdução ao executar Olá obter Power BI inserido, você precisa toocreate pelo menos um **coleta de espaço de trabalho** na sua assinatura do Azure. toolearn como toocreate uma **coleta de espaço de trabalho** em Olá Portal do Azure, consulte [guia de Introdução ao Power BI inserido](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Configurar o aplicativo de exemplo hello

Vamos examinar a configuração de seu aplicativo de exemplo Visual Studio desenvolvimento ambiente tooaccess Olá componentes necessários toorun hello.

1. Baixe e descompacte Olá [Power BI inserido - integrar um relatório em um aplicativo web](http://go.microsoft.com/fwlink/?LinkId=761493) exemplo no GitHub.
2. Abra **PowerBI-embedded.sln** no Visual Studio. Talvez seja necessário Olá tooexecute **pacote de atualização** do hello Console de Gerenciador de pacote do NuGET em ordem tooupdate Olá pacotes usados nesta solução.
3. Compile a solução de saudação.
4. Executar Olá **ProvisionSample** aplicativo de console. No aplicativo de console do exemplo hello, você provisiona um espaço de trabalho e importa um arquivo PBIX.
5. tooprovision um novo **espaço de trabalho**, selecione a opção 1, **gerenciamento coleção**e, em seguida, selecione a opção 6, **provisionar um novo espaço de trabalho**
6. tooimport um novo **relatório**, selecione a opção 2, **relatório gerenciamento**e, em seguida, selecione a opção 3, **arquivo de importação PBIX Desktop em um espaço de trabalho**.

7. Insira o nome da sua **Coleção de Espaços de Trabalho** e a sua **Chave de Acesso**. Você pode obter em Olá **Portal do Azure**. toolearn mais informações sobre como tooget o **chave de acesso**, consulte [chaves de acesso de API do modo de exibição Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) na introdução ao Microsoft Power BI inserido.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Copie e salve Olá recém-criado **ID do espaço de trabalho** toouse neste artigo. Depois de saudação **ID do espaço de trabalho** é criado, você pode encontrar hello **Portal do Azure**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. o arquivo de tooimport um PBIX em seu **espaço de trabalho**, selecione a opção **6. Importe o arquivo da Área de Trabalho PBIX em um espaço de trabalho existente**. Se você não tiver um PBIX útil do arquivo, você pode baixar Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Se solicitado, insira um nome amigável para o **Conjunto de Dados**.

Você verá uma resposta semelhante a essa:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Se o arquivo PBIX contiver quaisquer conexões de consulta direta, execute cadeias de caracteres da conexão Olá opção tooupdate 7.

Neste ponto, um relatório PBIX do Power BI é importado para o seu **Espaço de Trabalho**. Agora, vamos dar uma olhada em como Olá toorun **Power BI inserido** obter o aplicativo web de exemplo de Introdução.

## <a name="run-hello-sample-web-app"></a>Execute o aplicativo de web de exemplo hello
Olá aplicativo web de exemplo é um aplicativo de exemplo que renderiza relatórios importados para o **espaço de trabalho**. Aqui está como tooconfigure Olá aplicativo web de exemplo.

1. Em Olá **inserido PowerBI** solução do Visual Studio, direito clique Olá **EmbedSample** aplicativo web e escolha **definir como projeto de inicialização**.
2. Em **Web. config**, em Olá **EmbedSample** aplicativo web, edite Olá **appSettings**: **AccessKey**,  **WorkspaceCollection** nome, e **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Executar Olá **EmbedSample** aplicativo web.

Quando você executar Olá **EmbedSample** aplicativo web, o painel de navegação esquerdo Olá deve conter um **relatórios** menu. relatório de saudação tooview você importou, expanda **relatórios**e clique em um relatório. Se você importou Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547), aplicativo de web de exemplo hello teria esta aparência:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Depois de clicar em um relatório, Olá **EmbedSample** aplicativo web deve ser algo isso:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Explorar o código de exemplo hello

Olá **Microsoft Power BI inserido** exemplo é um aplicativo da web de exemplo que mostra como toointegrate **Power BI** relatórios em seu aplicativo. Ele usa um Model-View-Controller (MVC) práticas recomendadas de toodemonstrate de padrão de design. Esta seção destaca as partes do código de exemplo hello que você pode explorar em hello **inserido PowerBI** solução de aplicativo web. Olá, o padrão Model-View-Controller (MVC) separa modelagem de saudação do domínio hello, apresentação hello e as ações de saudação com base na entrada do usuário em três classes separadas: modelo, exibição e controle. toolearn mais sobre o MVC, consulte [Saiba mais sobre ASP.NET](http://www.asp.net/mvc).

Olá **Microsoft Power BI inserido** código de exemplo é separado da seguinte maneira. Cada seção inclui o nome do arquivo hello no hello PowerBI embedded.sln solução para que você pode localizar facilmente código Olá no exemplo hello.

> [!NOTE]
> Esta seção é um resumo Olá códigos de exemplo que mostra como o código de saudação foi escrito. saudação de tooview completa de exemplo, carregue a solução Olá PowerBI embedded.sln no Visual Studio.

### <a name="model"></a>Modelo

exemplo Hello tem um **ReportsViewModel** e **ReportViewModel**.

**ReportsViewModel.cs**: representa relatórios do Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: representa um relatório do Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Cadeia de conexão

cadeia de caracteres de conexão Olá deve ser Olá formato a seguir:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Usar atributos comuns de servidor e de banco de dados falhará. Por exemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Visualizar

Olá **exibição** gerencia a exibição de saudação do Power BI **relatórios** e um Power BI **relatório**.

**Reports.cshtml**: iterar **Model.Reports** toocreate um **ActionLink**. Olá **ActionLink** é composto da seguinte maneira:

| Parte | Descrição |
| --- | --- |
| Title |Nome do relatório de saudação. |
| QueryString |Um link de toohello ID do relatório. |

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

Report.cshtml: Definir Olá **Model.AccessToken**, e Olá expressão Lambda para **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**: cria um PowerBIClient que passa um **token de aplicativo**. Um JSON Web Token (JWT) é gerada a partir Olá **chave de assinatura** tooget Olá **credenciais**. Olá **credenciais** é usada toocreate uma instância de **PowerBIClient**. Quando tiver uma instância de **PowerBIClient**, você poderá chamar GetReports() e GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

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


Tarefa<ActionResult> Report(string reportId)

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

### <a name="integrate-a-report-into-your-app"></a>Integrar um relatório em seu aplicativo

Depois que você tiver um **relatório**, você usa um **IFrame** tooembed Olá Power BI **relatório**. Aqui está um trecho de código do powerbi.js no hello **Microsoft Power BI inserido** exemplo.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filtrar relatórios inseridos no seu aplicativo

Você pode filtrar um relatório inserido usando uma sintaxe de URL. toodo isso, você adiciona um **$filter** consultar o parâmetro de cadeia de caracteres com um **eq** operador tooyour iFrame src url com hello filtro especificado. Aqui está a sintaxe de consulta de filtro hello:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} não pode incluir espaços ou caracteres especiais. Olá {fieldValue} aceita um único valor categórico.  

## <a name="see-also"></a>Consulte também

[Cenários comuns do Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Criar um novo relatório de um conjunto de dados](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)
