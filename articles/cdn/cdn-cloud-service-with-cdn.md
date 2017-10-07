---
title: "aaaIntegrate um serviço de nuvem do Azure com o Azure CDN | Microsoft Docs"
description: "Saiba como toodeploy um serviço de nuvem que serve o conteúdo de um ponto de extremidade CDN do Azure integrado"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a> Integrar um serviço de nuvem à CDN do Azure
Um serviço de nuvem pode ser integrado com a CDN do Azure, que serve o conteúdo do local do serviço de nuvem hello. Isso proporciona abordagem Olá vantagens a seguir:

* Implantar e atualizar, de maneira fácil, imagens, scripts e folhas de estilo nos diretórios de projetos de seu serviço de nuvem
* Atualizar facilmente os pacotes do NuGet Olá em seu serviço de nuvem, como jQuery ou versões de inicialização
* Gerenciar seu aplicativo Web o servido de CDN conteúdo e todos os do hello mesma interface do Visual Studio
* Fluxo de trabalho de implantação unificado para seu aplicativo Web e o conteúdo fornecido por CDN
* Integrar agrupamento e minificação ASP.NET à CDN do Azure

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste tutorial, você aprenderá a:

* [Integrar um ponto de extremidade da CDN do Azure a seu serviço de nuvem e fornecer conteúdo estático em suas páginas Web por meio da CDN do Azure](#deploy)
* [Definir configurações de cache para conteúdo estático em seu serviço de nuvem](#caching)
* [Fornecer conteúdo por ações do controlador na CDN do Azure](#controller)
* [Sirvam agrupados e minimizada conteúdo por meio do Azure CDN enquanto preserva a experiência no Visual Studio de depuração de script hello](#bundling)
* [Configurar o fallback de seus scripts e CSS quando a CDN do Azure estiver offline](#fallback)

## <a name="what-you-will-build"></a>O que você compilará
Você implantar uma função Web de serviço de nuvem usando o padrão de saudação modelo do ASP.NET MVC, adicionar conteúdo tooserve do código de uma CDN do Azure integrados, como uma imagem, resultados de ação do controlador e saudação padrão arquivos JavaScript e CSS e também gravar saudação de tooconfigure de código mecanismo de fallback para pacotes atendidas no evento de saudação que Olá CDN está offline.

## <a name="what-you-will-need"></a>O que será necessário
Este tutorial tem Olá pré-requisitos a seguir:

* Uma [conta do Microsoft Azure](/account/)
* Visual Studio 2015 com [SDK do Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Você precisa de uma conta do Azure toocomplete neste tutorial:
> 
> * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados até você pode manter a conta de saudação e usar serviços do Azure, como sites de livre.
> * Você pode [ativar benefícios para assinantes do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Todos os meses, sua assinatura do MSDN oferece créditos que podem ser usados para serviços pagos do Azure.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Implantar um serviço de nuvem
Nesta seção, você implantar o modelo de aplicativo do ASP.NET MVC na função de Web do serviço de nuvem do Visual Studio 2015 tooa de padrão de saudação e, em seguida, integrá-lo com um novo ponto de extremidade CDN. Siga as instruções de saudação abaixo:

1. No Visual Studio 2015, crie um novo serviço de nuvem do Azure na barra de menus Olá indo muito**arquivo > Novo > projeto > nuvem > serviço de nuvem do Azure**. Dê um nome a ele e clique em **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Selecione **função Web ASP.NET** e clique em Olá  **>**  botão. Clique em OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Selecione **MVC** e clique em **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Agora, publica este tooan de função Web serviço de nuvem do Azure. Projeto de serviço de nuvem hello e selecione **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Se você ainda não entrou no Microsoft Azure, clique em Olá **adicionar uma conta...**  Olá suspensa e clique em **adicionar uma conta** item de menu.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. Em Olá página de entrada, entrar com hello conta da Microsoft usada tooactivate sua conta do Azure.
7. Após ter entrado, clique em **Avançar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Se você ainda não tiver criado uma conta de armazenamento ou um serviço de nuvem, o Visual Studio o ajudará a criar ambos. Em Olá **criar serviço de nuvem e conta** caixa de diálogo, nome do tipo hello serviço desejado e região desejada Olá select. Em seguida, clique em **Criar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. No hello página de configurações de publicação, verifique se a configuração de saudação e clique em **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > o processo de publicação Olá para serviços de nuvem demora muito. Olá habilitar a implantação da Web para a opção de todas as funções pode tornar a depuração muito mais rápido de serviço de nuvem, fornecendo atualizações rápida (mas temporária) tooyour funções da Web. Para obter mais informações sobre essa opção, consulte [publicando um serviço de nuvem usando ferramentas do Azure Olá](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Olá quando **Log de atividades do Microsoft Azure** mostra que o status de publicação está **concluído**, você criará um ponto de extremidade CDN que esteja integrado com esse serviço de nuvem.
   
   > [!WARNING]
   > Se, após a publicação, o serviço de nuvem Olá implantado exibe uma tela de erro, é provável que porque está usando o serviço de nuvem Olá que você implantou um [sistema operacional que não inclui o .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Você pode contornar esse problema [Implantando o .NET 4.5.2 como uma tarefa de inicialização](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Criar um novo perfil CDN
Um perfil CDN é um conjunto de pontos de extremidade CDN.  Cada perfil contém um ou mais pontos de extremidade CDN.  Você poderá toouse tooorganize de vários perfis seus pontos de extremidade CDN, o domínio da internet, aplicativo web ou algum outro critério.

> [!TIP]
> Se você já tiver um perfil CDN que você deseja toouse para este tutorial, vá muito[criar um novo ponto de extremidade CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Criar um novo ponto de extremidade CDN
**toocreate um novo ponto de extremidade CDN para sua conta de armazenamento**

1. Em Olá [Portal de gerenciamento](https://portal.azure.com), navegar tooyour perfil CDN.  Você pode ter-fixado toohello painel na etapa anterior hello.  Se você não, você pode encontrá-lo clicando **procurar**, em seguida, **perfis CDN**, e clicando no perfil Olá planejar tooadd seu ponto de extremidade.
   
    folha de perfil CDN Olá aparece.
   
    ![Perfil CDN][cdn-profile-settings]
2. Clique em Olá **Adicionar ponto de extremidade** botão.
   
    ![Adicionar botão de ponto de extremidade][cdn-new-endpoint-button]
   
    Olá **adicionar um ponto de extremidade** folha é exibida.
   
    ![Adicionar folha de ponto de extremidade][cdn-add-endpoint]
3. Insira um **Nome** para esse ponto de extremidade CDN.  Esse nome será usado tooaccess seus recursos armazenados em cache no domínio Olá `<EndpointName>.azureedge.net`.
4. Em Olá **tipo de origem** lista suspensa, selecione *serviço de nuvem*.  
5. Em Olá **nome de host de origem** lista suspensa, selecione o seu serviço de nuvem.
6. Mantenha os padrões de saudação para **caminho de origem**, **cabeçalho de host de origem**, e **porta de origem/protocolo**.  Você deve especificar pelo menos um protocolo (HTTP ou HTTPS).
7. Clique em Olá **adicionar** toocreate botão Olá novo ponto de extremidade.
8. Depois que o ponto de extremidade de saudação é criado, ele aparece em uma lista de pontos de extremidade para o perfil de saudação. modo de exibição de lista Olá mostra Olá URL toouse tooaccess em cache o conteúdo, bem como domínio de origem de saudação.
   
    ![Ponto de extremidade CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > ponto de extremidade de saudação não estará imediatamente disponível para uso.  Pode demorar até minutos too90 para Olá toopropagate de registro por meio da rede CDN hello. Os usuários que tente imediatamente o nome de domínio toouse Olá CDN podem receber o código de status 404 até que o conteúdo de saudação está disponível por meio de saudação CDN.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Saudação de teste ponto de extremidade CDN
Quando a saudação status de publicação é **concluído**, abra uma janela do navegador e navegue muito**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Em minha configuração, essa URL é:

    http://camservice.azureedge.net/Content/bootstrap.css

Que corresponde a toohello URL de origem no ponto de extremidade CDN Olá a seguir:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Quando você navega muito**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, dependendo de seu navegador, será toodownload solicitada ou abra Olá bootstrap.css que origem do seu aplicativo Web publicado.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

De maneira semelhante, você pode acessar qualquer URL acessível publicamente em **http://*&lt;nomedoServiço>*.cloudapp.net/**, diretamente de seu ponto de extremidade CDN. Por exemplo:

* Um arquivo. js do caminho de /Script Olá
* Qualquer arquivo de conteúdo de saudação /Content caminho
* Qualquer controller/action
* Se a cadeia de caracteres de consulta hello está habilitada no ponto de extremidade CDN, qualquer URL com cadeias de caracteres de consulta

Na verdade, com hello acima de configuração, você pode hospedar o serviço de nuvem inteiro de saudação do  **http://*&lt;cdnName >*.azureedge.net/**. Se navegar muito**http://camservice.azureedge.net/ * *, obter resultado de ação de saudação da casa/índice.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Isso não significa, no entanto, que é sempre uma boa ideia tooserve um serviço de nuvem inteira por meio da CDN do Azure. 

Um CDN com otimização de entrega estático não necessariamente acelerar a entrega de ativos dinâmicos que não devem toobe armazenado em cache ou são atualizados com muita frequência, desde que Olá CDN deve puxar uma nova versão do ativo de saudação do servidor de origem Olá frequentemente. Para este cenário, você pode habilitar [aceleração de Site dinâmico](cdn-dynamic-site-acceleration.md) otimização (DSA) no ponto de extremidade CDN que usa vários toospeed técnicas a entrega de ativos dinâmicos não armazenável em cache. 

Se você tiver um site com uma mistura de conteúdo estático e dinâmico, você pode escolher tooserve seu conteúdo estático de CDN com um tipo de otimização estáticas (por exemplo, entrega geral web) e o conteúdo dinâmico tooserve diretamente do servidor de origem hello, ou por meio de uma CDN ponto de extremidade com otimização de DSA ativado caso a caso. toothat final, você já viu como arquivos de conteúdo individuais tooaccess do ponto de extremidade CDN hello. Vou mostrar como tooserve uma ação do controlador específico por meio de um ponto de extremidade CDN específico no servir conteúdo de ações do controlador por meio da CDN do Azure.

alternativa de saudação é toodetermine que conteúdo tooserve da CDN do Azure em uma base por caso no serviço de nuvem. toothat final, você já viu como arquivos de conteúdo individuais tooaccess do ponto de extremidade CDN hello. Vou mostrar como tooserve uma ação do controlador específico por meio de Olá ponto de extremidade CDN na [oferecer conteúdo de ações do controlador por meio do Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configurar opções de cache para arquivos estáticos em seu serviço de nuvem
Com a integração do Azure CDN no serviço de nuvem, você pode especificar como deseja estático toobe conteúdo armazenado em cache no ponto de extremidade CDN hello. toodo isso, abra *Web. config* de sua função Web do projeto (por exemplo, WebRole1) e adicionar um `<staticContent>` elemento muito`<system.webServer>`. Olá XML abaixo configura Olá cache tooexpire em 3 dias.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Quando você faz isso, todos os arquivos estáticos em seu serviço de nuvem observará Olá mesma regra em seu cache CDN. Para ter um controle mais granular das configurações de cache, adicione um arquivo *Web.config* a uma pasta e adicione suas configurações. Por exemplo, adicionar um *Web. config* arquivo toohello *\Content* pasta e substitua Olá conteúdo com hello XML a seguir:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Essa configuração faz com que todos os arquivos estáticos do hello *\Content* toobe pasta armazenada em cache por 15 dias.

Para obter mais informações sobre como Olá tooconfigure `<clientCache>` elemento, consulte [Cache do cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

Em [oferecer conteúdo de ações do controlador por meio do Azure CDN](#controller), também mostrarei como você pode definir configurações de cache para resultados de ação do controlador no hello cache CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Fornecer conteúdo por meio de ações do controlador por meio da CDN do Azure
Quando você integra uma função de Web do serviço de nuvem com o Azure CDN, é relativamente fácil tooserve conteúdo de ações do controlador por meio de saudação do Azure CDN. Diferente que atende a sua nuvem de serviço diretamente por meio do Azure CDN (mostrado acima), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra como toodo com divertido controlador MemeGenerator [reduzindo a latência em Olá web com hello CDN do Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Eu vou somente reproduzir isso aqui.

Suponha que no seu serviço de nuvem você deseja memes toogenerate com base em uma imagem Chuck Norris jovens (foto por [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) esta aparência:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Você tem um simples `Index` ação que permite que os clientes de saudação toospecify superlativos de saudação na imagem hello, gera Olá meme depois que eles lançar toohello ação. Como é Chuck Norris, você esperaria toobecome essa página totalmente populares globalmente. Este é um bom exemplo do fornecimento de conteúdo semidinâmico com a CDN do Azure.

Siga as etapas de saudação acima toosetup esta ação de controlador:

1. Em Olá *\Controllers* pasta, crie um novo arquivo. cs chamado *MemeGeneratorController.cs* e substituir Olá conteúdo com hello código a seguir. Ser-se parte destacada Olá de tooreplace com seu nome CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Clique com botão direito no padrão de saudação `Index()` ação e selecione **adicionar exibição**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Aceite as configurações de saudação abaixo e clique em **adicionar**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Olá abrir nova *Views\MemeGenerator\Index.cshtml* e substitua conteúdo Olá Olá HTML simple a seguir para enviar superlativos hello:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Publicar novamente o serviço de nuvem hello e navegue muito**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** em seu navegador.

Quando você enviar valores de formulário Olá muito`/MemeGenerator/Index`, Olá `Index_Post` método de ação retorna um link toohello `Show` método de ação com o identificador de entrada respectivos hello. Quando você clica em um link de hello, atingir Olá código a seguir:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Se o depurador local estiver conectado, você obterá Olá experiência de depuração normal com um local de redirecionamento. Se ele estiver em execução no serviço de nuvem hello, ele será redirecionado para:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Que corresponde a toohello URL de origem no ponto de extremidade CDN a seguir:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Você pode usar Olá `OutputCacheAttribute` atributo Olá `Generate` toospecify de método como resultado da ação Olá deve ser armazenada em cache, que aceita a CDN do Azure. código de saudação abaixo especificar uma expiração de cache de 1 hora (3.600 segundos).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Da mesma forma, você pode servir o conteúdo de qualquer ação do controlador em seu serviço de nuvem por meio de seu CDN do Azure, com a opção de cache de saudação desejada.

Na próxima seção, Olá, mostrarei como tooserve Olá agrupadas e minimizada CSS por meio da CDN do Azure e scripts.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integrar agrupamento e minificação ASP.NET à CDN do Azure
Folhas de estilo CSS e scripts alterados com frequência e são fortes candidatas à saudação cache de CDN do Azure. Atendendo Olá toda função Web por meio de seu Azure CDN é toointegrate de maneira mais fácil de saudação empacotamento e minimização com CDN do Azure. No entanto, você não pode desejar toodo isso, mostrarei como toodo, preservando Olá desejado develper experiência de ASP.NET empacotamento e minimização, como:

* Ótima experiência no modo de depuração
* Implantação simplificada
* Atualizações imediatas tooclients para atualizações de versão de script/CSS
* Mecanismo de fallback quando ocorre falha em seu ponto de extremidade CDN
* Minimizar modificações de código

Em Olá **WebRole1** projeto que você criou no [integrar um ponto de extremidade CDN do Azure com seu site do Azure e servir conteúdo estático das páginas da Web do Azure CDN](#deploy), abra *App_Start\ BundleConfig.cs* e dar uma olhada Olá `bundles.Add()` chamadas de método.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Olá primeiro `bundles.Add()` instrução adiciona um pacote de script no diretório virtual Olá `~/bundles/jquery`. Em seguida, abra *exibições \ compartilhadas\_cshtml* toosee como marca de pacote de script hello é renderizada. Você deve ser capaz de toofind Olá seguinte linha de código Razor:

    @Scripts.Render("~/bundles/jquery")

Quando esse código Razor é executado na função de Web do Azure hello, ele processará uma `<script>` marca Olá script a seguir toohello semelhante pacote:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

No entanto, quando ele é executado no Visual Studio digitando `F5`, ele processará individualmente a cada arquivo de script no pacote de saudação (no caso de Olá acima, somente um arquivo de script está no pacote de saudação):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Isso permite que você toodebug Olá código JavaScript do ambiente de desenvolvimento (agrupamento) de conexões de cliente simultâneas e melhorando arquivo download desempenho (minimização) em produção. É toopreserve um ótimo recurso com integração do Azure CDN. Além disso, desde que o pacote de saudação renderizada já contém uma cadeia de caracteres de versão gerado automaticamente, você deseja tooreplicate funcionalidade assim Olá sempre que você atualize sua versão de jQuery através do NuGet, ele pode ser atualizado no lado do cliente hello, assim como é possível.

Siga as próximas etapas Olá toointegration ASP.NET empacotamento e minimização com seu ponto de extremidade CDN.

1. Em *App_Start\BundleConfig.cs*, modificar Olá `bundles.Add()` métodos toouse outro [construtor pacote](http://msdn.microsoft.com/library/jj646464.aspx), que especifica um endereço CDN. toodo Olá isso, substitua `RegisterBundles` definição de método com hello código a seguir:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Ser tooreplace se `<yourCDNName>` com nome de saudação do seu CDN do Azure.
   
    Em palavras simples, você está definindo `bundles.UseCdn = true` e adicionados a um pacote de tooeach URL CDN concebido cuidadosamente. Por exemplo, Olá primeiro construtor no código hello:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    Olá igual é:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Este construtor informa ASP.NET empacotamento e minimização toorender arquivos de script individuais quando depurado localmente, mas use Olá especificado script tooaccess de saudação do endereço CDN em questão. No entanto, observe duas importantes características dessa URL da CDN criada cuidadosamente:
   
   * saudação de origem para esta URL CDN é `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que é realmente Olá diretório virtual do pacote de script hello em seu serviço de nuvem.
   * Como você está usando o construtor CDN, Olá marca de script CDN para o pacote de saudação não contém Olá gerado automaticamente a cadeia de caracteres de versão no hello renderizado URL. Você deve gerar uma cadeia de caracteres de versão exclusivo manualmente sempre que o pacote de script hello é modificado tooforce perder um cache em seu CDN do Azure. AT Olá mesmo tempo, essa cadeia de caracteres de versão exclusivo deve permanecem constante durante a vida Olá Olá implantação toomaximize de acertos do cache em seu CDN do Azure após a implantação do pacote de saudação.
   * Olá a cadeia de caracteres de consulta v = < w.x.y. z > recebimentos de *Properties\AssemblyInfo.cs* em seu projeto de função Web. Você pode ter um fluxo de trabalho de implantação que inclui incrementando a versão do assembly hello toda vez que você publicar tooAzure. Ou, você pode modificar apenas *Properties\AssemblyInfo.cs* em sua cadeia de versão do projeto tooautomatically incremento Olá sempre que você criar, usando o caractere curinga de saudação ' *'. Por exemplo:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Qualquer outra estratégia toostreamline gerar uma cadeia de caracteres exclusiva durante saudação de uma implantação funcionará aqui.
2. Republicar Olá nuvem acesso e serviço Olá página inicial.
3. Saudação de modo de exibição código HTML para a página de saudação. Você deve ser capaz de toosee Olá URL CDN renderizado com uma cadeia de caracteres de versão exclusivo toda vez que você publicar novamente o serviço de nuvem tooyour alterações. Por exemplo:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. No Visual Studio, depurar o serviço em nuvem no Visual Studio Olá digitando `F5`.,
5. Saudação de modo de exibição código HTML para a página de saudação. Você ainda verá cada arquivo de script renderizado individualmente, para que possa ter uma experiência de depuração consistente no Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Mecanismo de fallback para URLs da CDN
Quando o ponto de extremidade CDN do Azure falha por algum motivo, você deseja que sua página da Web toobe inteligente suficiente tooaccess seu servidor da Web de origem como opção de fallback Olá para carregar JavaScript ou inicialização. É grave o suficiente toolose imagens no seu site devido a indisponibilidade de tooCDN, mas a funcionalidade de página fundamental de toolose muito mais grave fornecidos por seus scripts e folhas de estilo.

Olá [pacote](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contém uma propriedade chamada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que habilita o mecanismo de fallback tooconfigure Olá para falha CDN. toouse essa propriedade, siga Olá etapas abaixo:

1. No seu projeto de função Web, abra *App_Start\BundleConfig.cs*, em que você adicionou uma URL de CDN em cada [construtor pacote](http://msdn.microsoft.com/library/jj646464.aspx)e faça o seguinte Olá realçado altera tooadd toohello de mecanismo de fallback pacotes padrão:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Quando `CdnFallbackExpression` é não nulo, script é injetado tootest Olá HTML se o pacote de saudação é carregado com êxito e, se não, acessar Olá pacote diretamente do servidor de Web de origem hello. Essa propriedade deve toobe tooa JavaScript expressão de conjunto testa se o respectivo pacote CDN Olá é carregado corretamente. expressão de saudação necessário tootest difere de cada pacote de conteúdo de acordo toohello. Para pacotes de padrão de saudação acima:
   
   * `window.jquery` é definido em jquery-{version}.js
   * `$.validator` é definido em jquery.validate.js
   * `window.Modernizr` é definido em modernizer-{version}.js
   * `$.fn.modal` é definido em bootstrap.js
     
     Você deve ter notado que eu não definiu CdnFallbackExpression para Olá `~/Cointent/css` pacote. Isso ocorre porque atualmente não há uma [bug na otimização](https://aspnetoptimization.codeplex.com/workitem/104) que insere um `<script>` marca Olá esperado do CSS fallback em vez da saudação `<link>` marca.
     
     Há, no entanto, um bom [Fallback de Grupo de Estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferecido pelo [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. solução alternativa de saudação toouse para CSS, crie um novo arquivo. cs no seu projeto de função Web *App_Start* pasta chamada *StyleBundleExtensions.cs*e substituir seu conteúdo com hello [código de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. Em *App_Start\StyleFundleExtensions.cs*, renomeie o nome da função do hello namespace tooyour da Web (por exemplo, **WebRole1**).
4. Voltar muito`App_Start\BundleConfig.cs` e modificar Olá última `bundles.Add` instrução com hello código realçado a seguir:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Esse novo método de extensão usa Olá ideia mesmo tooinject script hello HTML toocheck Olá DOM para Olá um nome de classe correspondente, o nome da regra e o valor de regra definida no hello CSS pacote e o servidor vão toohello back origem Web se ele falhar toofind correspondência de saudação.
5. Publica serviço de nuvem Olá novamente e acesso Olá home page.
6. Saudação de modo de exibição código HTML para a página de saudação. Você deve encontrar injetado scripts semelhantes toohello seguinte:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Observe que o script inserido para o pacote CSS Olá ainda contém vestígios errôneo de saudação do hello `CdnFallbackExpression` propriedade na linha de saudação:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Mas como a primeira parte Olá Olá | | expressão sempre retornará verdadeira (na linha de saudação diretamente acima), a função de Document hello nunca será executado.

## <a name="more-information"></a>Mais informações
* [Visão geral de hello Azure Content Delivery Network (CDN)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Usando o Azure CDN](cdn-create-new-endpoint.md)
* [Agrupamento e minificação ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
