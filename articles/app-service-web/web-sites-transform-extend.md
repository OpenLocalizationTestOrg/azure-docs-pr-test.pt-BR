---
title: "Configurações avançadas e extensões de aplicativo Web do Serviço de Aplicativo do Azure"
description: "Use as declarações de XDT (Transformação de documento XML) para transformar o arquivo ApplicationHost.config em seu aplicativo Web do Serviço de Aplicativo do Azure e adicionar extensões privadas para habilitar ações de administração personalizadas."
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
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="38ec7-103">Configurações avançadas e extensões de aplicativo Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="38ec7-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="38ec7-104">Ao usar declarações XDT ([Transformação de Documento XML](http://msdn.microsoft.com/library/dd465326.aspx)), você pode transformar o arquivo [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) em seu aplicativo Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="38ec7-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="38ec7-105">Também é possível usar declarações XDT para adicionar extensões de site privadas a fim de habilitar ações de administração de aplicativo Web personalizadas.</span><span class="sxs-lookup"><span data-stu-id="38ec7-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="38ec7-106">Este artigo inclui uma extensão de aplicativo Web do Gerenciador de PHP de exemplo, que habilita o gerenciamento das configurações de PHP por meio de uma interface da Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="38ec7-107"><a id="transform"></a>Configuração avançada por meio de ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="38ec7-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="38ec7-108">A plataforma do Serviço de Aplicativo fornece flexibilidade e controle para configuração de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="38ec7-109">Embora o arquivo de configuração ApplicationHost.config do IIS padrão não esteja disponível para edição direta no Serviço de Aplicativo, a plataforma dá suporte a um modelo de transformação ApplicationHost.config declarativo com base em XDT (Transformação de documento XML).</span><span class="sxs-lookup"><span data-stu-id="38ec7-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="38ec7-110">Para aproveitar essa funcionalidade de transformação, você cria um arquivo ApplicationHost.xdt com conteúdo XDT e o coloca na raiz do site (d:\home\site) no [Console do Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="38ec7-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="38ec7-111">Talvez seja necessário reiniciar o aplicativo Web para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="38ec7-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="38ec7-112">O exemplo applicationHost.xdt a seguir mostra como adicionar uma nova variável de ambiente personalizada para um aplicativo Web que utilize PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="38ec7-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="38ec7-113">Um arquivo de log com status e detalhes de transformação está disponível na raiz FTP em LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="38ec7-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="38ec7-114">Para ver outros exemplos, veja [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="38ec7-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="38ec7-115">**Observação**</span><span class="sxs-lookup"><span data-stu-id="38ec7-115">**Note**</span></span><br />
<span data-ttu-id="38ec7-116">Os elementos da lista de módulos em `system.webServer` não podem ser removidos nem reorganizados, mas é possível fazer adições à lista.</span><span class="sxs-lookup"><span data-stu-id="38ec7-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="38ec7-117"><a id="extend"></a> Estender seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="38ec7-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="38ec7-118"><a id="overview"></a> Visão geral das extensões privadas de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="38ec7-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="38ec7-119">O Serviço de Aplicativo dá suporte a extensões de aplicativo Web como um ponto de extensibilidade para ações administrativas.</span><span class="sxs-lookup"><span data-stu-id="38ec7-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="38ec7-120">Na verdade, alguns recursos de plataforma do Serviço de Aplicativo são implementados como extensões pré-instaladas.</span><span class="sxs-lookup"><span data-stu-id="38ec7-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="38ec7-121">Embora as extensões de plataforma pré-instaladas não possam ser modificadas, é possível criar e configurar extensões privadas para seu próprio aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="38ec7-122">Essa funcionalidade também se baseia em declarações XDT.</span><span class="sxs-lookup"><span data-stu-id="38ec7-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="38ec7-123">As etapas principais para a criação de uma extensão privada de aplicativo Web são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="38ec7-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="38ec7-124">**Conteúdo**de extensão de aplicativo Web: criar qualquer aplicativo Web ao qual o Serviço de Aplicativo dá suporte</span><span class="sxs-lookup"><span data-stu-id="38ec7-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="38ec7-125">**Declaração**de extensão de aplicativo Web: criar um arquivo ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="38ec7-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="38ec7-126">**Implantação** de extensão de aplicativo Web: colocar o conteúdo na pasta SiteExtensions, em `root`</span><span class="sxs-lookup"><span data-stu-id="38ec7-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="38ec7-127">Os links internos para o aplicativo Web devem apontar para um caminho relativo ao caminho de aplicativo especificado no arquivo ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="38ec7-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="38ec7-128">Qualquer alteração feita ao arquivo ApplicationHost.xdt exige uma reciclagem do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="38ec7-129">**Observação**: informações adicionais sobre esses elementos-chave estão disponíveis em [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="38ec7-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="38ec7-130">Um exemplo detalhado está incluído para ilustrar as etapas para criar e habilitar uma extensão privada de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="38ec7-131">O código-fonte do exemplo Gerenciador de PHP a seguir pode ser baixado de [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="38ec7-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="38ec7-132"><a id="SiteSample"></a> Exemplo de extensão de aplicativo Web: Gerenciador de PHP</span><span class="sxs-lookup"><span data-stu-id="38ec7-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="38ec7-133">O Gerenciador de PHP é uma extensão de aplicativo Web que permite que os administradores de aplicativo Web exibam e definam facilmente suas configurações de PHP usando uma interface da Web em vez de precisar modificar arquivos .ini PHP diretamente.</span><span class="sxs-lookup"><span data-stu-id="38ec7-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="38ec7-134">Entre os arquivos de configuração comuns para PHP estão o arquivo php. ini localizado em Arquivos de Programas e o arquivo .user.ini localizado na pasta raiz do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="38ec7-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="38ec7-135">Como o arquivo php.ini não é editável diretamente na plataforma do Serviço de Aplicativo, a extensão do Gerenciador de PHP usa o arquivo .user.ini para aplicar alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="38ec7-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="38ec7-136"><a id="PHPwebapp"></a> O aplicativo Web do Gerenciador de PHP</span><span class="sxs-lookup"><span data-stu-id="38ec7-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="38ec7-137">A seguir está a página inicial de implantação do Gerenciador de PHP:</span><span class="sxs-lookup"><span data-stu-id="38ec7-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="38ec7-139">Como você pode ver, uma extensão do aplicativo Web é exatamente como um aplicativo Web normal, mas com um arquivo ApplicationHost.xdt adicional colocado na pasta raiz do aplicativo Web (mais detalhes sobre o arquivo ApplicationHost.xdt estão disponíveis na próxima seção deste artigo).</span><span class="sxs-lookup"><span data-stu-id="38ec7-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="38ec7-140">A extensão Gerenciador de PHP foi criada usando-se o modelo de aplicativo Web MVC 4 do ASP.NET do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38ec7-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="38ec7-141">A exibição a seguir do Gerenciador de Soluções mostra a estrutura da extensão Gerenciador de PHP.</span><span class="sxs-lookup"><span data-stu-id="38ec7-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="38ec7-143">A única lógica especial necessária para E/S de arquivo é indicar onde o diretório wwwroot do aplicativo Web está localizado.</span><span class="sxs-lookup"><span data-stu-id="38ec7-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="38ec7-144">Como mostra o seguinte exemplo de código, a variável de ambiente "HOME" indica o caminho da raiz do aplicativo Web, e o caminho wwwroot pode ser construído acrescentando-se "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="38ec7-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="38ec7-145">Já com o caminho do diretório, você pode usar operações de E/S de arquivo regulares para ler e gravar arquivos.</span><span class="sxs-lookup"><span data-stu-id="38ec7-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="38ec7-146">Um ponto de cuidado em relação às extensões do aplicativo Web se refere à identificação de links internos.</span><span class="sxs-lookup"><span data-stu-id="38ec7-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="38ec7-147">Se tiver quaisquer links em seus arquivos HTML que indiquem caminhos absolutos para links internos no aplicativo Web, você deverá garantir que esses links sejam acrescentados ao início do nome da extensão, como sua raiz.</span><span class="sxs-lookup"><span data-stu-id="38ec7-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="38ec7-148">Isso é necessário porque a raiz da extensão agora é "/`[your-extension-name]`/" em vez de ser apenas "/", logo, todo link interno deve ser atualizado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="38ec7-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="38ec7-149">Por exemplo, suponhamos que o código inclua um link para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="38ec7-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="38ec7-150">Quando o link fizer parte de uma extensão de aplicativo Web, esse link deverá estar no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="38ec7-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="38ec7-151">Você pode contornar esse requisito usando apenas caminhos relativos no aplicativo Web ou, no caso de aplicativos do ASP.NET, usando o método `@Html.ActionLink` , que cria os links apropriados para você.</span><span class="sxs-lookup"><span data-stu-id="38ec7-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="38ec7-152"><a id="XDT"></a> O arquivo applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="38ec7-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="38ec7-153">O código da extensão do aplicativo Web fica em %HOME%\SiteExtensions\[nome-da-extensão].</span><span class="sxs-lookup"><span data-stu-id="38ec7-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="38ec7-154">Chamaremos ele de a raiz da extensão.</span><span class="sxs-lookup"><span data-stu-id="38ec7-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="38ec7-155">Para registrar a extensão do aplicativo Web com o arquivo applicationHost.config, você precisa colocar um arquivo chamado ApplicationHost.xdt na raiz da extensão.</span><span class="sxs-lookup"><span data-stu-id="38ec7-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="38ec7-156">O conteúdo do arquivo ApplicationHost.xdt deve ser conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="38ec7-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="38ec7-157">O nome que você seleciona como o nome da extensão deve ser igual ao nome da pasta raiz da extensão.</span><span class="sxs-lookup"><span data-stu-id="38ec7-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="38ec7-158">Isso tem o efeito de adicionar um novo caminho de aplicativo à lista de sites `system.applicationHost` no site SCM.</span><span class="sxs-lookup"><span data-stu-id="38ec7-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="38ec7-159">O site SCM é um ponto de extremidade de administração de site com credenciais de acesso específicas.</span><span class="sxs-lookup"><span data-stu-id="38ec7-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="38ec7-160">Tem a URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="38ec7-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="38ec7-161"><a id="deploy"></a> Implantação de extensão de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="38ec7-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="38ec7-162">Para instalar a extensão de aplicativo Web, você pode usar FTP para copiar todos os arquivos do seu aplicativo Web para a pasta `\SiteExtensions\[your-extension-name]` do aplicativo Web no qual você deseja instalar a extensão.</span><span class="sxs-lookup"><span data-stu-id="38ec7-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="38ec7-163">Não se esqueça de copiar o arquivo ApplicationHost.xdt para esse local também.</span><span class="sxs-lookup"><span data-stu-id="38ec7-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="38ec7-164">Reinicie o aplicativo Web para habilitar a extensão.</span><span class="sxs-lookup"><span data-stu-id="38ec7-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="38ec7-165">Você deve ser capaz de ver a extensão do aplicativo Web em:</span><span class="sxs-lookup"><span data-stu-id="38ec7-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="38ec7-166">Observe que a URL se parece com a URL do aplicativo Web, exceto por usar HTTPS e conter ".scm".</span><span class="sxs-lookup"><span data-stu-id="38ec7-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="38ec7-167">É possível desabilitar todas as extensões (não pré-instaladas) privadas do seu aplicativo Web durante o desenvolvimento e investigações adicionando uma configuração de aplicativo com a chave `WEBSITE_PRIVATE_EXTENSIONS` e um valor de `0`.</span><span class="sxs-lookup"><span data-stu-id="38ec7-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="38ec7-168">Se você deseja começar a usar o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38ec7-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="38ec7-169">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="38ec7-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="38ec7-170">O que mudou</span><span class="sxs-lookup"><span data-stu-id="38ec7-170">What's changed</span></span>
* <span data-ttu-id="38ec7-171">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="38ec7-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

