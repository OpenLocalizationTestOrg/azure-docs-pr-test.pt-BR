---
title: "configurações e extensões avançadas de aaaAzure aplicativo do serviço de aplicativo web"
description: "Use Transformation(XDT) de documento XML declarações tootransform Olá arquivo applicationHost. config em seu serviço de aplicativo do Azure web app e tooadd extensões privadas tooenable administração personalizadas Ações."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="f9275-103">Configurações avançadas e extensões de aplicativo Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f9275-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="f9275-104">Usando [transformação de documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declarações (XDT), você pode transformar Olá [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) arquivo em seu aplicativo web no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9275-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="f9275-105">Você também pode usar XDT declarações tooadd extensões privadas tooenable da web personalizado administração ações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9275-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="f9275-106">Este artigo inclui uma extensão de aplicativo Web do Gerenciador de PHP de exemplo, que habilita o gerenciamento das configurações de PHP por meio de uma interface da Web.</span><span class="sxs-lookup"><span data-stu-id="f9275-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="f9275-107"><a id="transform"></a>Configuração avançada por meio de ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="f9275-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="f9275-108">Olá plataforma do serviço de aplicativo fornece flexibilidade e controle de configuração de aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="f9275-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="f9275-109">Embora o arquivo de configuração de IIS applicationHost. config padrão Olá não está disponível para edição direta no serviço de aplicativo, plataforma Olá dá suporte a um modelo declarativo de transformação de applicationHost. config com base na transformação de documento XML (XDT).</span><span class="sxs-lookup"><span data-stu-id="f9275-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="f9275-110">tooleverage essa funcionalidade de transformação, crie um arquivo de ApplicationHost.xdt com XDT conteúdo e coloque sob a raiz do site hello (d:\home\site) no hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="f9275-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="f9275-111">Talvez seja necessário toorestart Olá Web App para efeito de tootake de alterações.</span><span class="sxs-lookup"><span data-stu-id="f9275-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="f9275-112">Olá applicationHost.xdt exemplo a seguir mostra como o aplicativo que usa PHP 5.4 da web de tooadd um novo tooa de variável de ambiente personalizado.</span><span class="sxs-lookup"><span data-stu-id="f9275-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="f9275-113">Um arquivo de log com detalhes e status de transformação está disponível de raiz FTP de saudação em LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="f9275-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="f9275-114">Para ver outros exemplos, veja [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="f9275-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="f9275-115">**Observação**</span><span class="sxs-lookup"><span data-stu-id="f9275-115">**Note**</span></span><br />
<span data-ttu-id="f9275-116">Elementos da lista de saudação de módulos em `system.webServer` não podem ser removidos ou reordenados, mas a lista de toohello adições são possíveis.</span><span class="sxs-lookup"><span data-stu-id="f9275-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="f9275-117"><a id="extend"></a> Estender seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f9275-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="f9275-118"><a id="overview"></a> Visão geral das extensões privadas de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f9275-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="f9275-119">O Serviço de Aplicativo dá suporte a extensões de aplicativo Web como um ponto de extensibilidade para ações administrativas.</span><span class="sxs-lookup"><span data-stu-id="f9275-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="f9275-120">Na verdade, alguns recursos de plataforma do Serviço de Aplicativo são implementados como extensões pré-instaladas.</span><span class="sxs-lookup"><span data-stu-id="f9275-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="f9275-121">Enquanto as extensões da plataforma pré-instalados Olá não podem ser modificadas, você pode criar e configurar extensões privadas para seu próprio aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f9275-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="f9275-122">Essa funcionalidade também se baseia em declarações XDT.</span><span class="sxs-lookup"><span data-stu-id="f9275-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="f9275-123">para criar uma extensão do aplicativo web privada principais etapas de saudação são seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f9275-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="f9275-124">**Conteúdo**de extensão de aplicativo Web: criar qualquer aplicativo Web ao qual o Serviço de Aplicativo dá suporte</span><span class="sxs-lookup"><span data-stu-id="f9275-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="f9275-125">**Declaração**de extensão de aplicativo Web: criar um arquivo ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="f9275-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="f9275-126">Extensão de aplicativo da Web **implantação**: colocar o conteúdo na pasta de SiteExtensions Olá em`root`</span><span class="sxs-lookup"><span data-stu-id="f9275-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="f9275-127">Links internos para o aplicativo web de saudação deve apontar tooa caminho relativo toohello aplicativo caminho especificado no arquivo de ApplicationHost.xdt hello.</span><span class="sxs-lookup"><span data-stu-id="f9275-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="f9275-128">Qualquer arquivo de ApplicationHost.xdt toohello alteração requer uma reciclagem de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f9275-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="f9275-129">**Observação**: informações adicionais sobre esses elementos-chave estão disponíveis em [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="f9275-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="f9275-130">Um exemplo detalhado é incluído tooillustrate Olá etapas para criar e habilitar uma extensão do aplicativo web privada.</span><span class="sxs-lookup"><span data-stu-id="f9275-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="f9275-131">Olá código-fonte de exemplo do Gerenciador do PHP hello que segue pode ser baixado do [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="f9275-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="f9275-132"><a id="SiteSample"></a> Exemplo de extensão de aplicativo Web: Gerenciador de PHP</span><span class="sxs-lookup"><span data-stu-id="f9275-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="f9275-133">O Gerenciador do PHP é uma extensão do aplicativo web que permite que os administradores de aplicativo web tooeasily exibir e definir suas configurações de PHP usando uma interface da web em vez de ter arquivos. ini toomodify PHP diretamente.</span><span class="sxs-lookup"><span data-stu-id="f9275-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="f9275-134">Arquivos de configuração comuns para PHP incluem arquivo ini de Olá localizado em arquivos de programa e hello. user.ini arquivo localizado na pasta raiz de saudação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f9275-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="f9275-135">Como arquivo php.ini de saudação não pode ser editado diretamente no hello plataforma do serviço de aplicativo, Olá extensão do Gerenciador do PHP usa hello. user.ini arquivo tooapply alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="f9275-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="f9275-136"><a id="PHPwebapp"></a>saudação de aplicativo de web do Gerenciador do PHP</span><span class="sxs-lookup"><span data-stu-id="f9275-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="f9275-137">a seguir Olá é Olá home page do hello implantação do Gerenciador do PHP:</span><span class="sxs-lookup"><span data-stu-id="f9275-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="f9275-139">Como você pode ver, uma extensão do aplicativo web é como um aplicativo web regular, mas com um arquivo ApplicationHost.xdt adicional na pasta raiz de saudação do aplicativo web de saudação (mais detalhes sobre o arquivo de ApplicationHost.xdt Olá estão disponíveis na próxima seção, Olá deste artigo).</span><span class="sxs-lookup"><span data-stu-id="f9275-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="f9275-140">saudação de extensão do Gerenciador do PHP foi criada usando o modelo de aplicativo de Web do Visual Studio ASP.NET MVC 4 hello.</span><span class="sxs-lookup"><span data-stu-id="f9275-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="f9275-141">Olá seguinte modo de exibição no Gerenciador de soluções mostra estrutura Olá Olá extensão do Gerenciador do PHP.</span><span class="sxs-lookup"><span data-stu-id="f9275-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="f9275-143">Olá somente uma lógica especial necessária para e/s de arquivo é tooindicate onde hello diretório wwwroot do aplicativo web de saudação está localizado.</span><span class="sxs-lookup"><span data-stu-id="f9275-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="f9275-144">Como a seguir mostra exemplo de código, Olá Olá variável de ambiente "HOME" indica Olá caminho de raiz do aplicativo web e o caminho de wwwroot Olá pode ser construído anexando "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="f9275-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="f9275-145">Depois de ter o caminho do diretório hello, você pode usar tooread de operações de e/s de arquivos regulares e gravar toofiles.</span><span class="sxs-lookup"><span data-stu-id="f9275-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="f9275-146">Um ponto de cuidado com extensões de aplicativo web considera a manipulação de saudação de links internos.</span><span class="sxs-lookup"><span data-stu-id="f9275-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="f9275-147">Se você tiver todos os links nos arquivos HTML que fornecem caminhos absolutos toointernal links em seu aplicativo web, você deve garantir que esses links são prefixados com seu nome de extensão como sua raiz.</span><span class="sxs-lookup"><span data-stu-id="f9275-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="f9275-148">Isso é necessário porque Olá raiz para a sua extensão agora é "/`[your-extension-name]`/" em vez de ser links apenas "/", portanto qualquer interno deve ser atualizado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f9275-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="f9275-149">Por exemplo, suponha que seu código inclui o seguinte de toohello um link:</span><span class="sxs-lookup"><span data-stu-id="f9275-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="f9275-150">Quando o link de saudação fizer parte de uma extensão de aplicativo da web, link Olá deve ser Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9275-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="f9275-151">Você pode contornar esse requisito usando somente a caminhos relativos no seu aplicativo web, ou em Olá caso de aplicativos ASP.NET, usando Olá `@Html.ActionLink` método que cria os links apropriados Olá para você.</span><span class="sxs-lookup"><span data-stu-id="f9275-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="f9275-152"><a id="XDT"></a>arquivo de applicationHost.xdt Olá</span><span class="sxs-lookup"><span data-stu-id="f9275-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="f9275-153">código de saudação para a sua extensão de aplicativo web entra em %HOME%\SiteExtensions\[seu nome de extensão].</span><span class="sxs-lookup"><span data-stu-id="f9275-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="f9275-154">Chamaremos raiz desse extensão hello.</span><span class="sxs-lookup"><span data-stu-id="f9275-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="f9275-155">tooregister sua extensão do aplicativo web com o arquivo applicationHost config hello, você precisa tooplace um arquivo chamado ApplicationHost.xdt na raiz da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9275-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="f9275-156">conteúdo de saudação do arquivo de ApplicationHost.xdt Olá deve ser da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9275-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="f9275-157">Selecione como o nome da extensão de nome de saudação deve ter Olá mesmo nome como a pasta raiz de extensão.</span><span class="sxs-lookup"><span data-stu-id="f9275-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="f9275-158">Isso tem o efeito de saudação de adicionar um novo toohello de caminho do aplicativo `system.applicationHost` lista de sites no site SCM hello.</span><span class="sxs-lookup"><span data-stu-id="f9275-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="f9275-159">site SCM Olá é um ponto de extremidade de administração de site com as credenciais de acesso específicas.</span><span class="sxs-lookup"><span data-stu-id="f9275-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="f9275-160">Ele tem Olá URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f9275-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="f9275-161"><a id="deploy"></a> Implantação de extensão de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f9275-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="f9275-162">tooinstall sua extensão do aplicativo web, você pode usar todos os arquivos de saudação do seu toohello de aplicativo web FTP toocopy `\SiteExtensions\[your-extension-name]` pasta do aplicativo web de saudação no qual você deseja a extensão de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f9275-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="f9275-163">Ser se toocopy Olá ApplicationHost.xdt toothis local do arquivo também.</span><span class="sxs-lookup"><span data-stu-id="f9275-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="f9275-164">Reinicie sua extensão de saudação do tooenable de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f9275-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="f9275-165">Você deve ser capaz de toosee sua extensão do aplicativo web em:</span><span class="sxs-lookup"><span data-stu-id="f9275-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="f9275-166">Observe que Olá que URL parece com hello URL para seu aplicativo web, exceto que ela usa HTTPS e contém ".scm".</span><span class="sxs-lookup"><span data-stu-id="f9275-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="f9275-167">É extensões toodisable privada todos os possíveis (não pré-instalado) para seu aplicativo web durante o desenvolvimento e investigações adicionando configurações de um aplicativo com chave Olá `WEBSITE_PRIVATE_EXTENSIONS` e um valor de `0`.</span><span class="sxs-lookup"><span data-stu-id="f9275-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="f9275-168">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9275-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f9275-169">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="f9275-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f9275-170">O que mudou</span><span class="sxs-lookup"><span data-stu-id="f9275-170">What's changed</span></span>
* <span data-ttu-id="f9275-171">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f9275-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

