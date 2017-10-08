---
title: "aplicativo de web móvel aaaDeploy um ASP.NET MVC 5 no serviço de aplicativo do Azure"
description: "Um tutorial que ensina como toodeploy uma tooAzure de aplicativo web do serviço de aplicativo móvel usando o recursos no ASP.NET MVC 5 aplicativo da web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Implantar um aplicativo Web móvel ASP.NET MVC 5 no Serviço de Aplicativo do Azure
Este tutorial irá ensiná-Olá Noções básicas de como toobuild um ASP.NET MVC 5 web aplicativo amigáveis para dispositivos móveis e implantá-lo tooAzure do serviço de aplicativo. Para este tutorial, você precisa [Visual Studio Express 2013 para Web] [ Visual Studio Express 2013] ou a edição professional saudação do Visual Studio se ele já está instalado. Você pode usar [Visual Studio 2015] mas capturas de tela de saudação serão diferentes e você deve usar modelos do hello ASP.NET 4. x.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>O que você vai construir
Para este tutorial, você adicionará recursos móveis toohello listagem de conferência aplicativo simples que é fornecido no hello [projeto inicial][StarterProject]. Olá seguinte captura de tela mostra Olá ASP.NET sessões no aplicativo hello concluída, como visto no emulador de navegador Olá nas ferramentas de desenvolvedor F12 do Internet Explorer 11.

![][FixedSessionsByTag]

Você pode usar ferramentas de desenvolvedor Olá F12 do Internet Explorer 11 e hello [ferramenta Fiddler] [ Fiddler] toohelp depurar seu aplicativo. 

## <a name="skills-youll-learn"></a>Qualificações que você aprenderá
Eis o que você vai aprender:

* Como toopublish toouse Visual Studio 2013 seu aplicativo web diretamente tooa de aplicativo web no serviço de aplicativo do Azure.
* Como modelos Olá ASP.NET MVC 5 usam o framework de inicialização de CSS Olá para melhorar a exibição em dispositivos móveis
* Como toocreate específicas para dispositivos móveis exibições tootarget específico navegadores de dispositivos móveis, como iPhone hello e Android
* Como toocreate responsivo exibições (exibições que respondem toodifferent navegadores em todos os dispositivos)

## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento Olá
Configurar seu ambiente de desenvolvimento, instalando hello Azure SDK para .NET 2.5.1 ou posterior. 

1. Olá tooinstall SDK do Azure para .NET, clique o link de saudação abaixo. Se você não tiver o Visual Studio 2013 instalado, ele será instalado por um link de saudação. Este tutorial requer o Visual Studio 2013. [SDK do Azure para o Visual Studio 2013][AzureSDKVs2013]
2. Na janela do Web Platform Installer hello, clique em **instalar** e prosseguir com a instalação de saudação.

Também será necessário um emulador do navegador móvel. Qualquer um dos seguintes Olá funcionará:

* Emulador do navegador nas [ferramentas de desenvolvedor do Internet Explorer 11 F12][EmulatorIE11] (usado em todas as capturas de tela do navegador móvel). Ele possui predefinições de cadeia de caracteres de agente de usuário para Windows Phone 8, Windows Phone 7 e Apple iPad.
* Emulador de navegador nas [DevTools do Google Chrome][EmulatorChrome]. Contém predefinições para vários dispositivos Android, e também para Apple iPhone, Apple iPad e Amazon Kindle Fire. Ele também emula eventos de toque.
* [Emulador do Opera para dispositivos móveis][EmulatorOpera]

Projetos do Visual Studio com C\# código-fonte é tooaccompany disponível neste tópico:

* [Download do projeto inicial][StarterProject]
* [Download do projeto concluído][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Implantar o aplicativo de web do Azure do hello starter projeto tooan
1. Baixe o aplicativo de listagem de conferência hello [projeto inicial][StarterProject].
2. Em seguida, no Windows Explorer, clique no arquivo ZIP de saudação baixado e escolha *propriedades*.
3. Em Olá **propriedades** caixa de diálogo caixa, escolha Olá **desbloquear** botão. (Desbloqueio impede que um aviso de segurança que ocorre quando você tenta toouse um *. zip* arquivo que você baixou da web hello.)
4. Arquivo ZIP de saudação e selecione **extrair tudo** para descompactar o arquivo hello. 
5. No Visual Studio, abra Olá *C#\Mvc5Mobile.sln* arquivo.
6. No Gerenciador de soluções, clique com botão direito hello e clique em **publicar**.
   
   ![][DeployClickPublish]
7. Em Publicar Web, clique em **Serviço de Aplicativo do Microsoft Azure**.
   
   ![][DeployClickWebSites]
8. Se você ainda não tiver feito logon no Azure, clique em **Adicionar uma conta**.
   
   ![][DeploySignIn]
9. Siga Olá prompts toolog em sua conta do Azure.
10. Olá caixa de diálogo serviço de aplicativo agora deve mostrar como conectado. Clique em **Novo**.
    
    ![][DeployNewWebsite]  
11. Em Olá **nome do aplicativo Web** , especifique um prefixo de nome exclusivo do aplicativo. O nome totalmente qualificado do aplicativo Web será *&lt;prefixo>*.azurewebsites.net. Além disso, especifique um novo nome de grupo de recursos em **Grupo de recursos**. Em seguida, clique em **novo** toocreate um novo plano de serviço de aplicativo.
    
    ![][DeploySiteSettings]
12. Configurar o novo plano de serviço de aplicativo hello e clique em **Okey**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Novamente na caixa de diálogo de criação de serviço de aplicativo hello, clique em **criar**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Depois hello recursos do Azure são criados, de diálogo Publicar Web hello será preenchido com as configurações de saudação para seu novo aplicativo. Clique em **Publicar**.
    
    ![][DeployPublishSite]
    
    Depois que o Visual Studio termina publicação Olá starter projeto toohello web do Azure aplicativo, o navegador de área de trabalho Olá abre toodisplay Olá web dinâmico aplicativo.
15. Iniciar o emulador do navegador de dispositivo móvel, copie Olá URL para o aplicativo de conferência hello (*<prefix>*. azurewebsites.net) no emulador do Windows hello e, em seguida, clique no botão superior direito e selecione **procurar por marca**. Se você estiver usando o Internet Explorer 11 como navegador padrão de saudação, basta tootype `F12`, em seguida, `Ctrl+8`e alterar o perfil de navegador Olá muito**do Windows Phone**. A imagem abaixo mostra Olá *AllTags* exibição no modo retrato (escolha **procurar por marca**).
    
    ![][AllTags]

> [!TIP]
> Enquanto você pode depurar seu aplicativo MVC 5 de dentro do Visual Studio, você pode publicar seu tooAzure de aplicativo da web novamente tooverify Olá ao vivo aplicativo web diretamente do seu navegador móvel ou um emulador de navegador.
> 
> 

exibição de saudação é muito legível em um dispositivo móvel. Você também já pode ver alguns dos efeitos visuais de saudação aplicados pela estrutura de inicialização CSS hello.
Clique em Olá **ASP.NET** link.

![][SessionsByTagASP.NET]

Olá modo de exibição ASP.NET é ajustado zoom toohello tela, que Bootstrap faz para você automaticamente. No entanto, você pode melhorar essa exibição toobetter naipe Olá navegador de dispositivo móvel. Por exemplo, Olá **data** coluna é difícil de ler. Posteriormente no tutorial hello, você alterará Olá *AllTags* exibir toomake-amigáveis para dispositivos móveis.

## <a name="bkmk_bootstrap"></a> Framework de CSS Bootstrap
A novidade no hello MVC 5 modelo é suporte interno a inicialização. Você já viu como ele melhora imediatamente Olá modos de exibição em seu aplicativo. Por exemplo, barra de navegação de saudação na parte superior da saudação é recolhível automaticamente quando a largura do navegador de saudação for menor. No navegador de área de trabalho hello, tente redimensionar a janela do navegador hello e ver como a barra de navegação Olá altera sua aparência. Este é o design de web responsivo Olá que é criado na inicialização.

toosee como aplicativo da Web de saudação seria sem inicialização, abra *aplicativo\_iniciar\\BundleConfig.cs* e comente as linhas de saudação que contenham *bootstrap.js* e *bootstrap.css*. Olá código a seguir mostra Olá duas últimas instruções de saudação `RegisterBundles` método após alteração hello:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Pressione `Ctrl+F5` aplicativo hello de toorun.

Observe a que barra de navegação recolhível que Olá agora é apenas uma lista não ordenada comum. Clique em **Procurar por marcação** novamente e clique em **ASP.NET**.
No modo de exibição de emulador móvel hello, você pode ver agora que já não é ajustado para zoom toohello tela e você deve rolar lateralmente na ordem toosee, Olá direita da tabela de saudação.

![][SessionsByTagASP.NETNoBootstrap]

Desfaça as alterações e atualizar Olá navegador móvel tooverify que a exibição de dispositivos móveis Olá foi restaurada.

Inicialização não é específico tooASP.NET MVC 5, e você pode tirar proveito desses recursos em um aplicativo web. Ele é, porém, um recurso interno do modelo de projeto MVC 5 do ASP.NET, de forma que o seu aplicativo Web MVC 5 pode, por padrão, aproveitar o Bootstrap.

Para obter mais informações sobre inicialização, vá toothe [Bootstrap] [ BootstrapSite] site.

Na próxima seção, Olá você verá como modos de exibição específicos tooprovide navegador móvel.

## <a name="bkmk_overrideviews"></a>Substituição de modos de exibição de hello, Layouts e exibições parciais
Você pode substituir qualquer modo de exibição (inclusive layouts e modos de exibição parciais) para navegadores de dispositivos móveis em geral, para um navegador móvel individual ou para qualquer navegador específico. Exibir do tooprovide uma específicas para dispositivos móveis, você pode copiar um arquivo de exibição e adicionar *. Mobile* toohello nome de arquivo. Por exemplo, toocreate móveis *índice* exibição, você pode copiar *exibições\\início\\cshtml* para *modos de exibição\\início\\ Index.Mobile.cshtml*.

Nesta seção, você criará um arquivo de layout específico para dispositivos móveis.

toostart, cópia *exibições\\compartilhado\\\_cshtml* para *exibições\\compartilhado\\\_Layout.Mobile.cshtml* . Abra  *\_Layout.Mobile.cshtml* e altere o título de saudação do **MVC5 aplicativo** muito**MVC5 aplicativo (móvel)**.

Em cada `Html.ActionLink` chamada para a barra de navegação hello, remova "Procurar por" em cada link *ActionLink*. Olá, código a seguir mostra Olá concluída `<ul class="nav navbar-nav">` marca de arquivo de layout para dispositivos móveis hello.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Saudação de cópia *exibições\\início\\AllTags.cshtml* o arquivo para *exibições\\início\\AllTags.Mobile.cshtml*. Abra o novo arquivo de saudação e altere o `<h2>` elemento de "Tags" muito "marcas (M)":

    <h2>Tags (M)</h2>

Procure toohello marcas página usando um navegador da área de trabalho e usar o emulador do navegador móvel. emulador de navegador móvel Olá mostra Olá duas alterações feitas (Olá título de  *\_Layout.Mobile.cshtml* e título de saudação do *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Por outro lado, exibição de área de trabalho Olá não foi alterada (com títulos de  *\_cshtml* e *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> Criar modos de exibição para um navegador específico
Além disso toomobile-área de trabalho específicas e exibições, você pode criar modos de exibição para um navegador individual. Por exemplo, você pode criar exibições que são específicas para iPhone hello ou navegador do Android hello. Nesta seção, você criará um layout para o navegador do iPhone hello e uma versão de iPhone do hello *AllTags* exibição.

Olá abrir *global. asax* de arquivos e adicionar Olá inferior toohello código a seguir o `Application_Start` método.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Este código define um novo modo de exibição denominado “iPhone”, que será comparado a todas as solicitações de entrada. Se a solicitação de entrada hello corresponder a condição definida (ou seja, se o agente do usuário Olá contém a cadeia de caracteres do hello "iPhone"), o ASP.NET MVC procurará exibições cujo nome contém o sufixo "iPhone".

> [!NOTE]
> Quando adicionar específicos de navegador móvel modos de exibição, como para iPhone e Android, ser se tooset Olá primeiro argumento muito`0` (inserir na parte superior de saudação da lista de saudação) toomake-se de que o modo de navegador específico Olá tem precedência sobre o modelo móveis Olá (*. Cshtml). Se o modelo móveis hello está na parte superior de saudação da lista de saudação em vez disso, ele será selecionado em seu modo de exibição desejado (Olá primeiro wins de correspondência e modelo móveis Olá corresponde a todos os navegadores móveis). 
> 
> 

No código de saudação, clique com botão direito `DefaultDisplayMode`, escolha **resolver**e, em seguida, escolha `using System.Web.WebPages;`. Isso adiciona uma referência toothe `System.Web.WebPages` namespace, que é o local onde o `DisplayModeProvider` e `DefaultDisplayMode` tipos são definidos.

![][ResolveDefaultDisplayMode]

Como alternativa, você pode adicionar apenas manualmente Olá toothe linha a seguir `using` seção do arquivo hello.

    using System.Web.WebPages;

Salve alterações de saudação. Copie o arquivo *Views\\Shared\\\_Layout.Mobile.cshtml* para *Views\\Shared\\\_Layout.iPhone.cshtml*. Abra o novo arquivo de saudação e, em seguida, altere o título de saudação do `MVC5 Application (Mobile)` para `MVC5 Application (iPhone)`.

Saudação de cópia *exibições\\início\\AllTags.Mobile.cshtml* o arquivo para *exibições\\início\\AllTags.iPhone.cshtml*. No novo arquivo de saudação, alterar Olá `<h2>` elemento de "marcas (M)" muito "marcas (iPhone)".

Execute o aplicativo hello. Executar um emulador navegador móvel, verifique se o agente do usuário está definido muito "iPhone" e procurar toohello *AllTags* exibição. Se você estiver usando o emulador Olá nas ferramentas de desenvolvedor F12 do Internet Explorer 11, configure a seguir toohello emulação:

* Perfil do navegador = **Windows Phone**
* Cadeia de caracteres de agente do usuário = **Personalizado**
* Cadeia de caracteres personalizada = **Apple-iPhone5C1/1001,525**

Olá, seguinte captura de tela mostra Olá *AllTags* exibição renderizada no emulador do Windows em ferramentas de desenvolvedor F12 do Internet Explorer 11 com a cadeia de caracteres de agente de usuário personalizada hello (Esta é uma cadeia de caracteres de agente de usuário do iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

No navegador de dispositivo móvel hello, selecione Olá **alto-falantes** link. Porque não há uma exibição móvel (*AllSpeakers.Mobile.cshtml*), exibir alto-falantes do saudação padrão (*AllSpeakers.cshtml*) é processado usando o modo de exibição de layout para dispositivos móveis hello ( *\_ Layout.Mobile.cshtml*). Conforme mostrado abaixo, título Olá **MVC5 aplicativo (móvel)** é definido em  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Globalmente você pode desabilitar o modo de exibição padrão (não móveis) da renderização dentro de um layout para dispositivos móveis, definindo `RequireConsistentDisplayMode` para `true` em Olá *exibições\\\_ViewStart.cshtml* arquivo, como este:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Quando `RequireConsistentDisplayMode` está definido muito`true`, layout móveis hello (*\_Layout.Mobile.cshtml*) é usado apenas para exibições móveis (ou seja, quando o arquivo de exibição é do formulário Olá  ***ViewName** . Cshtml*). Talvez você queira tooset `RequireConsistentDisplayMode` muito`true` se o layout para dispositivos móveis não funcionar bem com seus modos de exibição não móveis. Olá captura de tela abaixo mostra como Olá *alto-falantes* page renderiza quando `RequireConsistentDisplayMode` está definido muito`true` (sem Olá cadeia de caracteres "(móvel)" em Olá navegação barra na parte superior da saudação).

![][AllSpeakers_LayoutMobileOverridden]

Você pode desabilitar o modo de exibição consistente em um modo específico, definindo `RequireConsistentDisplayMode` muito`false` no arquivo de exibição de saudação. A seguinte marcação em Olá *exibições\\início\\AllSpeakers.cshtml* conjuntos de arquivos `RequireConsistentDisplayMode` muito`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

Esta seção que vimos como toocreate móveis layouts e modos de exibição e como toocreate layouts e modos de exibição para dispositivos específicos, como Olá iPhone.
No entanto, Olá principal vantagem do framework de inicialização CSS Olá é o layout dinâmico, o que significa que uma única folha de estilos pode ser aplicada de área de trabalho, telefone e tablet navegadores toocreate uma aparência consistente. Na próxima seção, Olá você verá como tooleverage inicializar amigáveis para dispositivos móveis toocreate modos de exibição.

## <a name="bkmk_Improvespeakerslist"></a>Melhorar Olá alto-falantes lista
Como você acabou de ver, Olá *alto-falantes* modo de exibição pode ser lido, mas Olá links são pequenos e tootap difícil em um dispositivo móvel. Nesta seção, você fará Olá *AllSpeakers* exibição amigáveis para dispositivos móveis, que exibe links grande, fácil de toque e contém um tooquickly da caixa de pesquisa localizar alto-falantes.

Você pode usar o hello Bootstrap [grupo de lista vinculada] [ linked list group] estilo para melhorar a saudação *alto-falantes* exibição. Em *exibições\\início\\AllSpeakers.cshtml*, substitua o conteúdo de saudação do arquivo de Razor de saudação com código de saudação abaixo.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Olá `class="list-group"` atributo Olá `<div>` marca aplica o estilo de lista de inicialização e hello `class="input-group-item"` atributo aplica-se o link de tooeach de estilo de item de lista de inicialização.

Atualize o navegador móvel hello. Olá atualizado exibição esta aparência:

![][AllSpeakersFixed]

Olá Bootstrap [grupo de lista vinculada] [ linked list group] estilo torna Olá caixa inteira para cada link clicável, que é uma experiência de usuário muito melhor. Alternar exibição da área de trabalho toothe e observar Olá aparência consistente.

![][AllSpeakersFixedDesktop]

Embora o modo de exibição de navegador móvel Olá melhorou, é difícil navegar longa lista Olá de alto-falantes. O Bootstrap não oferece uma funcionalidade de filtro de pesquisa pronta para uso, mas você pode adicionar uma utilizando poucas linhas de código. Você primeiro adiciona uma exibição de toohello da caixa de pesquisa e a ligar com hello código JavaScript para a função de filtro de saudação. Em *exibições\\início\\AllSpeakers.cshtml*, adicionar um \<formulário\> marca logo após Olá \<h2\> marca, conforme mostrado abaixo:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Observe que Olá `<form>` e `<input>` marcas ambos têm Olá Bootstrap estilos aplicados toothem. Olá `<span>` elemento adiciona uma inicialização [glyphicon] [ glyphicon] toothe caixa de pesquisa.

Em Olá *Scripts* pasta, adicione um arquivo JavaScript chamado *filter.js*. Abra o arquivo hello e cole Olá código a seguir para ele:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

Você também precisa tooinclude filter.js em seus pacotes registrados. Abra *aplicativo\_iniciar\\BundleConfig.cs* e alterar pacotes de saudação primeiro. Alterar o primeiro `bundles.Add` instrução (para Olá **jquery** pacote) tooinclude *Scripts\\filter.js*, da seguinte maneira:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Olá **jquery** pacote já é renderizado por padrão Olá  *\_Layout* exibição. Posteriormente, você pode utilizar Olá JavaScript mesmo código tooapply os modos de exibição de lista do filtro funcionalidade tooother.

Atualize o navegador móvel hello e vá toohello *AllSpeakers* exibição. Na caixa de pesquisa, digite “sc”. lista de alto-falantes Olá agora deve ser filtrada acordo com a cadeia de caracteres de pesquisa tooyour.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Melhorar Olá lista de marcas
Como Olá *alto-falantes* exibir, hello *marcas* modo de exibição pode ser lido, mas Olá links são pequeno e de difícil tootap em um dispositivo móvel. Você pode corrigir Olá *marcas* exibição Olá mesmo maneira corrigir Olá *alto-falantes* exibir, se você usar as alterações de código Olá descritas anteriormente, mas com os seguintes Olá `Html.ActionLink` sintaxe de método em  *Modos de exibição\\início\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Olá atualizados parece navegador de área de trabalho da seguinte maneira:

![][AllTagsFixedDesktop]

E Olá atualizado navegador móvel parece da seguinte maneira: 

![][AllTagsFixed]

> [!NOTE]
> Se você notar que formatação da lista original Olá ainda está em Olá navegador móvel e o estilo de inicialização adequado com tooyour esteja se perguntando, este é um artefato da sua anteriores ação toocreate móvel exibições específicas. No entanto, agora que você estiver usando Olá Bootstrap CSS framework toocreate um design responsivo web, vá head e remover essas exibições específicas para dispositivos móveis e modos de exibição de layout específicas para dispositivos móveis hello. Depois de você ter feito isso, navegador de dispositivo móvel atualizado Olá mostrará estilo Bootstrap hello.
> 
> 

## <a name="bkmk_improvedates"></a>Melhorar Olá lista de datas
Você pode melhorar Olá *datas* exibir como aprimorado Olá *alto-falantes* e *marcas* exibições se você usar alterações de código de saudação descritas anteriormente, mas com hello após `Html.ActionLink` sintaxe de método em *exibições\\início\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

A exibição atualizada do navegador móvel será como esta:

![][AllDatesFixed]

Você pode melhorar ainda mais o hello *datas* exibição, organizando os valores de data e hora Olá por data. Isso pode ser feito com hello Bootstrap [painéis] [ panels] de estilo. Substitua o conteúdo de saudação do hello *exibições\\início\\AllDates.cshtml* arquivo com o código a seguir:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Esse código cria um separado `<div class="panel panel-primary">` marca para cada data distinta na lista de Olá e usa Olá [grupo de lista vinculada] [ linked list group] para os respectivos links como antes. Aqui está o navegador móvel Olá aparência quando esse código é executado:

![][AllDatesFixed2]

Opção toohello área de trabalho no navegador. Novamente, observe a aparência consistente hello.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Melhorar Olá SessionsTable exibição
Nesta seção, você fará Olá *SessionsTable* exibir mais amigáveis para dispositivos móveis. Essa alteração é alterações anteriores de hello mais ampla.

No navegador de dispositivo móvel hello, toque em Olá **marca** botão e, em seguida, digite `asp` na caixa de pesquisa.

![][AllTagsFixedSearchByASP]

Toque em Olá **ASP.NET** link.

![][SessionsTableTagASP.NET]

Como você pode ver, a exibição de saudação é formatada como uma tabela, que é atualmente projetado toobe exibido no navegador de área de trabalho de saudação. No entanto, é um pouco difícil tooread em um navegador móvel. toofix isso, abra *exibições\\início\\SessionsTable.cshtml* e, em seguida, substitua conteúdo de saudação do arquivo hello código a seguir:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

código de saudação faz 3:

* usa Olá Bootstrap [grupo personalizado de lista vinculada] [ custom linked list group] tooformat Olá informações de sessão verticalmente, para que todas essas informações pode ser lidas em um navegador móvel (usando classes como lista de grupo-item-texto)
* aplica-se a saudação [sistema grade] [ grid system] toothe layout, portanto essa sessão Olá itens fluxo horizontalmente no navegador de área de trabalho hello e verticalmente no navegador de dispositivo móvel hello (usando a classe do hello col-md-4)
* Olá usa [utilitários responsivos] [ responsive utilities] para ocultar marcas de sessão hello quando exibido no navegador de dispositivo móvel hello (usando a classe de xs oculto de saudação)

Você também pode tocar uma título toogo toohello respectivos a sessão de link. imagem de saudação abaixo reflete as alterações de código hello.

![][FixedSessionsByTag]

sistema de inicialização grade Olá aplicadas automaticamente Organiza as sessões verticalmente no navegador móvel hello. Além disso, observe que as marcas de saudação não são mostradas. Opção toohello área de trabalho no navegador.

![][SessionsTableFixedTagASP.NETDesktop]

No navegador de área de trabalho Olá, observe que as marcas de saudação agora são exibidas. Além disso, você pode ver que sistema de inicialização grade Olá que você aplicou organiza os itens de sessão de saudação em duas colunas. Se você aumentar o navegador, você verá que organização Olá muda toothree colunas.

## <a name="bkmk_improvesessionbycode"></a>Melhorar Olá SessionByCode exibição
Por fim, você corrigirá Olá *SessionByCode* exibir toomake-amigáveis para dispositivos móveis.

No navegador de dispositivo móvel hello, toque em Olá **marca** botão e, em seguida, digite `asp` na caixa de pesquisa.

![][AllTagsFixedSearchByASP]

Toque em Olá **ASP.NET** link. As sessões de marca ASP.NET hello serão exibidas.

![][FixedSessionsByTag]

Escolha Olá **criando um aplicativo de página única com ASP.NET e AngularJS** link.

![][SessionByCode3-644]

modo de exibição da área de trabalho saudação padrão é bom, mas você pode melhorar a aparência de saudação facilmente usando alguns componentes de GUI de inicialização.

Abra *exibições\\início\\SessionByCode.cshtml* e substitua o conteúdo de saudação com hello marcação a seguir:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

nova marcação de saudação usa Bootstrap painéis definindo o estilo de modo de exibição móvel tooimprove hello. 

Atualize o navegador móvel hello. Olá imagem a seguir reflete as alterações de código de saudação que você acabou de criar:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Conclusão e revisão
Este tutorial mostrou como aplicativos de Web toouse ASP.NET MVC 5 toodevelop amigáveis para dispositivos móveis. Estão incluídos:

* Implantar um aplicativo de ASP.NET MVC 5 tooan aplicativo do serviço de aplicativo web
* Use layout de web responsivo toocreate de inicialização em seu aplicativo MVC 5
* Substituir layouts, modos de exibição e exibições parciais globalmente ou para um modo de exibição individual
* Controlar a imposição de layout e de substituição parcial usando a propriedade `RequireConsistentDisplayMode`
* Criar exibições que navegadores específicos, como o navegador do iPhone Olá de destino
* Aplicar estilos do Bootstrap no código Razor

## <a name="see-also"></a>Consulte também
* [9 princípios básicos do design da Web responsivo](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Blog oficial do Bootstrap][Official Bootstrap Blog]
* [Tutorial do Bootstrap no Twitter, feito pela Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Olá parque de inicialização][hello Bootstrap Playground]
* [Práticas recomendadas pelo W3C para Aplicativos Web Móveis][W3C Recommendation Mobile Web Application Best Practices]
* [Recomendação Candidata do W3C para consultas de mídia][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

