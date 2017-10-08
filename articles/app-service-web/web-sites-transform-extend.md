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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Configurações avançadas e extensões de aplicativo Web do Serviço de Aplicativo do Azure
Usando [transformação de documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declarações (XDT), você pode transformar Olá [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) arquivo em seu aplicativo web no serviço de aplicativo do Azure. Você também pode usar XDT declarações tooadd extensões privadas tooenable da web personalizado administração ações de aplicativo. Este artigo inclui uma extensão de aplicativo Web do Gerenciador de PHP de exemplo, que habilita o gerenciamento das configurações de PHP por meio de uma interface da Web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Configuração avançada por meio de ApplicationHost.config
Olá plataforma do serviço de aplicativo fornece flexibilidade e controle de configuração de aplicativo da web. Embora o arquivo de configuração de IIS applicationHost. config padrão Olá não está disponível para edição direta no serviço de aplicativo, plataforma Olá dá suporte a um modelo declarativo de transformação de applicationHost. config com base na transformação de documento XML (XDT).

tooleverage essa funcionalidade de transformação, crie um arquivo de ApplicationHost.xdt com XDT conteúdo e coloque sob a raiz do site hello (d:\home\site) no hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console). Talvez seja necessário toorestart Olá Web App para efeito de tootake de alterações.

Olá applicationHost.xdt exemplo a seguir mostra como o aplicativo que usa PHP 5.4 da web de tooadd um novo tooa de variável de ambiente personalizado.

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

Um arquivo de log com detalhes e status de transformação está disponível de raiz FTP de saudação em LogFiles\Transform.

Para ver outros exemplos, veja [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Observação**<br />
Elementos da lista de saudação de módulos em `system.webServer` não podem ser removidos ou reordenados, mas a lista de toohello adições são possíveis.

## <a id="extend"></a> Estender seu aplicativo Web
### <a id="overview"></a> Visão geral das extensões privadas de aplicativo Web
O Serviço de Aplicativo dá suporte a extensões de aplicativo Web como um ponto de extensibilidade para ações administrativas. Na verdade, alguns recursos de plataforma do Serviço de Aplicativo são implementados como extensões pré-instaladas. Enquanto as extensões da plataforma pré-instalados Olá não podem ser modificadas, você pode criar e configurar extensões privadas para seu próprio aplicativo web. Essa funcionalidade também se baseia em declarações XDT. para criar uma extensão do aplicativo web privada principais etapas de saudação são seguinte hello:

1. **Conteúdo**de extensão de aplicativo Web: criar qualquer aplicativo Web ao qual o Serviço de Aplicativo dá suporte
2. **Declaração**de extensão de aplicativo Web: criar um arquivo ApplicationHost.xdt
3. Extensão de aplicativo da Web **implantação**: colocar o conteúdo na pasta de SiteExtensions Olá em`root`

Links internos para o aplicativo web de saudação deve apontar tooa caminho relativo toohello aplicativo caminho especificado no arquivo de ApplicationHost.xdt hello. Qualquer arquivo de ApplicationHost.xdt toohello alteração requer uma reciclagem de aplicativo web.

**Observação**: informações adicionais sobre esses elementos-chave estão disponíveis em [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Um exemplo detalhado é incluído tooillustrate Olá etapas para criar e habilitar uma extensão do aplicativo web privada. Olá código-fonte de exemplo do Gerenciador do PHP hello que segue pode ser baixado do [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a> Exemplo de extensão de aplicativo Web: Gerenciador de PHP
O Gerenciador do PHP é uma extensão do aplicativo web que permite que os administradores de aplicativo web tooeasily exibir e definir suas configurações de PHP usando uma interface da web em vez de ter arquivos. ini toomodify PHP diretamente. Arquivos de configuração comuns para PHP incluem arquivo ini de Olá localizado em arquivos de programa e hello. user.ini arquivo localizado na pasta raiz de saudação do seu aplicativo web. Como arquivo php.ini de saudação não pode ser editado diretamente no hello plataforma do serviço de aplicativo, Olá extensão do Gerenciador do PHP usa hello. user.ini arquivo tooapply alterações de configuração.

#### <a id="PHPwebapp"></a>saudação de aplicativo de web do Gerenciador do PHP
a seguir Olá é Olá home page do hello implantação do Gerenciador do PHP:

![TransformSitePHPUI][TransformSitePHPUI]

Como você pode ver, uma extensão do aplicativo web é como um aplicativo web regular, mas com um arquivo ApplicationHost.xdt adicional na pasta raiz de saudação do aplicativo web de saudação (mais detalhes sobre o arquivo de ApplicationHost.xdt Olá estão disponíveis na próxima seção, Olá deste artigo).

saudação de extensão do Gerenciador do PHP foi criada usando o modelo de aplicativo de Web do Visual Studio ASP.NET MVC 4 hello. Olá seguinte modo de exibição no Gerenciador de soluções mostra estrutura Olá Olá extensão do Gerenciador do PHP.

![TransformSiteSolEx][TransformSiteSolEx]

Olá somente uma lógica especial necessária para e/s de arquivo é tooindicate onde hello diretório wwwroot do aplicativo web de saudação está localizado. Como a seguir mostra exemplo de código, Olá Olá variável de ambiente "HOME" indica Olá caminho de raiz do aplicativo web e o caminho de wwwroot Olá pode ser construído anexando "site\wwwroot":

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


Depois de ter o caminho do diretório hello, você pode usar tooread de operações de e/s de arquivos regulares e gravar toofiles.

Um ponto de cuidado com extensões de aplicativo web considera a manipulação de saudação de links internos.  Se você tiver todos os links nos arquivos HTML que fornecem caminhos absolutos toointernal links em seu aplicativo web, você deve garantir que esses links são prefixados com seu nome de extensão como sua raiz. Isso é necessário porque Olá raiz para a sua extensão agora é "/`[your-extension-name]`/" em vez de ser links apenas "/", portanto qualquer interno deve ser atualizado adequadamente. Por exemplo, suponha que seu código inclui o seguinte de toohello um link:

`"<a href="/Home/Settings">PHP Settings</a>"`

Quando o link de saudação fizer parte de uma extensão de aplicativo da web, link Olá deve ser Olá formulário a seguir:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Você pode contornar esse requisito usando somente a caminhos relativos no seu aplicativo web, ou em Olá caso de aplicativos ASP.NET, usando Olá `@Html.ActionLink` método que cria os links apropriados Olá para você.

#### <a id="XDT"></a>arquivo de applicationHost.xdt Olá
código de saudação para a sua extensão de aplicativo web entra em %HOME%\SiteExtensions\[seu nome de extensão]. Chamaremos raiz desse extensão hello.  

tooregister sua extensão do aplicativo web com o arquivo applicationHost config hello, você precisa tooplace um arquivo chamado ApplicationHost.xdt na raiz da extensão de saudação. conteúdo de saudação do arquivo de ApplicationHost.xdt Olá deve ser da seguinte maneira:

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

Selecione como o nome da extensão de nome de saudação deve ter Olá mesmo nome como a pasta raiz de extensão.

Isso tem o efeito de saudação de adicionar um novo toohello de caminho do aplicativo `system.applicationHost` lista de sites no site SCM hello. site SCM Olá é um ponto de extremidade de administração de site com as credenciais de acesso específicas. Ele tem Olá URL `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a> Implantação de extensão de aplicativo Web
tooinstall sua extensão do aplicativo web, você pode usar todos os arquivos de saudação do seu toohello de aplicativo web FTP toocopy `\SiteExtensions\[your-extension-name]` pasta do aplicativo web de saudação no qual você deseja a extensão de saudação tooinstall.  Ser se toocopy Olá ApplicationHost.xdt toothis local do arquivo também. Reinicie sua extensão de saudação do tooenable de aplicativo web.

Você deve ser capaz de toosee sua extensão do aplicativo web em:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Observe que Olá que URL parece com hello URL para seu aplicativo web, exceto que ela usa HTTPS e contém ".scm".

É extensões toodisable privada todos os possíveis (não pré-instalado) para seu aplicativo web durante o desenvolvimento e investigações adicionando configurações de um aplicativo com chave Olá `WEBSITE_PRIVATE_EXTENSIONS` e um valor de `0`.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

