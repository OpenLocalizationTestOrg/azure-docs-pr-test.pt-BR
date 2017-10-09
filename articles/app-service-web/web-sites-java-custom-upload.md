---
title: aaaUpload um tooAzure de aplicativo de web Java personalizado
description: "Este tutorial mostra como tooupload um personalizado Java web aplicativo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="c4830-103">Carregar um tooAzure de aplicativo de web Java personalizado</span><span class="sxs-lookup"><span data-stu-id="c4830-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="c4830-104">Este tópico explica como um Java personalizados de tooupload web aplicativo muito[do serviço de aplicativo do Azure] aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="c4830-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="c4830-105">Há informações que se aplicam a tooany site de Java ou aplicativo web e também alguns exemplos de aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="c4830-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="c4830-106">Observe que o Azure fornece um meio para a criação de aplicativos da web de Java usando a interface de configuração do Portal do Azure hello e hello Azure Marketplace, conforme documentado em [criar um aplicativo da web de Java no serviço de aplicativo do Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4830-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="c4830-107">Este tutorial destina-se a cenários em que você não deseja toouse hello Azure Portal configuração da interface do usuário ou hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c4830-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="c4830-108">Diretrizes de configuração</span><span class="sxs-lookup"><span data-stu-id="c4830-108">Configuration guidelines</span></span>
<span data-ttu-id="c4830-109">a seguir Olá descreve configurações de Olá esperadas para aplicativos de web Java personalizados no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4830-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="c4830-110">porta HTTP de saudação usada pelo Olá processo Java é atribuída dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="c4830-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="c4830-111">processo de saudação deve usar a porta de saudação da variável de ambiente Olá `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="c4830-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="c4830-112">Todos os escutam portas diferente de ouvinte HTTP única de saudação deve ser desabilitado.</span><span class="sxs-lookup"><span data-stu-id="c4830-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="c4830-113">No Tomcat, que inclui o desligamento hello, HTTPS e AJP portas.</span><span class="sxs-lookup"><span data-stu-id="c4830-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="c4830-114">contêiner de saudação deve toobe configurado para somente ao tráfego IPv4.</span><span class="sxs-lookup"><span data-stu-id="c4830-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="c4830-115">Olá **inicialização** de comando para o aplicativo hello precisa toobe definidas na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4830-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="c4830-116">Aplicativos que exigem a permissão de gravação de diretórios com precisam toobe localizado no diretório de conteúdo do aplicativo da web do Azure hello, que é **d:\home.**.</span><span class="sxs-lookup"><span data-stu-id="c4830-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="c4830-117">variável de ambiente Olá `HOME` refere-se tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="c4830-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="c4830-118">Você pode definir variáveis de ambiente conforme necessário no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4830-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="c4830-119">Configuração de httpPlatform do web.config</span><span class="sxs-lookup"><span data-stu-id="c4830-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="c4830-120">Olá, informações a seguir descrevem Olá **httpPlatform** formato em Web. config.</span><span class="sxs-lookup"><span data-stu-id="c4830-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="c4830-121">**arguments** (Padrão="").</span><span class="sxs-lookup"><span data-stu-id="c4830-121">**arguments** (Default="").</span></span> <span data-ttu-id="c4830-122">Argumentos toohello executável ou script especificado na Olá **processPath** configuração.</span><span class="sxs-lookup"><span data-stu-id="c4830-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="c4830-123">Exemplos (mostrados com **processPath** incluído):</span><span class="sxs-lookup"><span data-stu-id="c4830-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="c4830-124">**processPath** -toohello de caminho executável ou script que irá iniciar um processo que escuta solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="c4830-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="c4830-125">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="c4830-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="c4830-126">**rapidFailsPerMinute** (Padrão = 10.) Número de vezes que o processo de saudação especificado no **processPath** é permitido toocrash por minuto.</span><span class="sxs-lookup"><span data-stu-id="c4830-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="c4830-127">Se esse limite for excedido, **HttpPlatformHandler** interromperá a inicialização do processo Olá restante Olá minuto hello.</span><span class="sxs-lookup"><span data-stu-id="c4830-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="c4830-128">**requestTimeout** (Padrão="00:02:00".) Duração para a qual **HttpPlatformHandler** esperará por uma resposta do processo de saudação escutando `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="c4830-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="c4830-129">**startupRetryCount** (Padrão = 10.) Número de vezes **HttpPlatformHandler** tentará o processo de saudação toolaunch especificado no **processPath**.</span><span class="sxs-lookup"><span data-stu-id="c4830-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="c4830-130">Confira **startupTimeLimit** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c4830-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="c4830-131">**startupTimeLimit** (Padrão = 10 segundos.) Duração para a qual **HttpPlatformHandler** aguardará Olá executável/script toostart um processo que escuta na porta hello.</span><span class="sxs-lookup"><span data-stu-id="c4830-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="c4830-132">Se esse tempo limite for excedido, **HttpPlatformHandler** irá interromper o processo de saudação e tente toolaunch novamente **startupRetryCount** vezes.</span><span class="sxs-lookup"><span data-stu-id="c4830-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="c4830-133">**stdoutLogEnabled** (Padrão = "true".) Se true, **stdout** e **stderr** processo Olá especificado no hello **processPath** configuração será redirecionado toohello arquivo especificado no  **stdoutLogFile** (consulte **stdoutLogFile** seção).</span><span class="sxs-lookup"><span data-stu-id="c4830-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="c4830-134">**stdoutLogFile** (Padrão="d:\home\LogFiles\httpPlatformStdout.log".) Caminho de arquivo absoluto para o qual **stdout** e **stderr** do processo de saudação especificado em **processPath** será registrado.</span><span class="sxs-lookup"><span data-stu-id="c4830-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="c4830-135">`%HTTP_PLATFORM_PORT%`é um espaço reservado especial que deve toospecified como parte de **argumentos** ou como parte da saudação **httpPlatform** **environmentVariables** lista.</span><span class="sxs-lookup"><span data-stu-id="c4830-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="c4830-136">Isso será substituído por uma porta gerada internamente pelo **HttpPlatformHandler** para que o processo de saudação especificado por **processPath** pode escutar nesta porta.</span><span class="sxs-lookup"><span data-stu-id="c4830-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="c4830-137">Implantação</span><span class="sxs-lookup"><span data-stu-id="c4830-137">Deployment</span></span>
<span data-ttu-id="c4830-138">Os aplicativos web Java com base podem ser implantados facilmente na maior parte do hello que mesmo significa que é usados com aplicativos de web de serviços de informações da Internet (IIS) com base em hello.</span><span class="sxs-lookup"><span data-stu-id="c4830-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="c4830-139">FTP, Git e Kudu é todos suportado como mecanismos de implantação, conforme é Olá recurso SCM integrado para aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="c4830-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="c4830-140">O WebDeploy funciona como um protocolo, no entanto, como o Java não é desenvolvido no Visual Studio, o WebDeploy não é adequado para casos de uso de implantação de aplicativos Web Java.</span><span class="sxs-lookup"><span data-stu-id="c4830-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="c4830-141">Exemplos de configuração de aplicativos</span><span class="sxs-lookup"><span data-stu-id="c4830-141">Application configuration Examples</span></span>
<span data-ttu-id="c4830-142">Para Olá a seguir de aplicativos, um arquivo Web. config e hello configuração de aplicativo é fornecida como exemplos tooshow como tooenable seu aplicativo Java em aplicativos de Web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4830-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="c4830-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="c4830-143">Tomcat</span></span>
<span data-ttu-id="c4830-144">Existem duas variações no Tomcat que são fornecidas com o serviço de aplicativo Web de aplicativos, ainda é instâncias específicas do cliente tooupload bem possível.</span><span class="sxs-lookup"><span data-stu-id="c4830-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="c4830-145">A seguir, um exemplo de uma instalação do Tomcat com uma JVM (Máquina Virtual Java) diferente.</span><span class="sxs-lookup"><span data-stu-id="c4830-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="c4830-146">Em Olá lado Tomcat, há algumas alterações de configuração que precisam toobe feita.</span><span class="sxs-lookup"><span data-stu-id="c4830-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="c4830-147">Olá XML precisa tooset toobe editado:</span><span class="sxs-lookup"><span data-stu-id="c4830-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="c4830-148">Shutdown port = -1</span><span class="sxs-lookup"><span data-stu-id="c4830-148">Shutdown port = -1</span></span>
* <span data-ttu-id="c4830-149">HTTP connector port = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="c4830-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="c4830-150">HTTP connector address = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="c4830-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="c4830-151">Comente os conectores HTTPS e AJP</span><span class="sxs-lookup"><span data-stu-id="c4830-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="c4830-152">configuração de IPv4 saudação também pode ser definida no arquivo Catalina de saudação onde você pode adicionar`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="c4830-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="c4830-153">Chamadas de Direct3d não têm suporte em Aplicativos Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4830-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="c4830-154">toodisable, adicione Olá seguinte opção Java deve seu aplicativo fazer essas chamadas:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="c4830-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="c4830-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="c4830-155">Jetty</span></span>
<span data-ttu-id="c4830-156">Como é o caso de Olá para Tomcat, os clientes podem carregar suas próprias instâncias para Jetty.</span><span class="sxs-lookup"><span data-stu-id="c4830-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="c4830-157">No caso de saudação de execução instalação completa de saudação do Jetty, configuração de saudação teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c4830-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="c4830-158">configuração do Jetty Hello precisa toobe alterado em Olá start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="c4830-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="c4830-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="c4830-159">Springboot</span></span>
<span data-ttu-id="c4830-160">Em ordem tooget um Springboot aplicativo em execução, você precisa tooupload seu arquivo JAR ou WAR e adicione Olá após o arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="c4830-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="c4830-161">arquivo Web. config de saudação se encaixa na pasta wwwroot hello.</span><span class="sxs-lookup"><span data-stu-id="c4830-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="c4830-162">No Web. config de saudação ajustar o arquivo JAR do hello argumentos toopoint tooyour, no hello seguir o arquivo JAR do exemplo hello está localizado em Olá na pasta wwwroot também.</span><span class="sxs-lookup"><span data-stu-id="c4830-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="c4830-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="c4830-163">Hudson</span></span>
<span data-ttu-id="c4830-164">Nosso teste usado Olá war Hudson 3.1.2 e Olá a instância padrão do Tomcat 7.0.50, mas sem usando coisas que tooset Olá da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c4830-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="c4830-165">Como Hudson é uma ferramenta de compilação do software, é aconselhável tooinstall-la no dedicado instâncias onde hello **AlwaysOn** sinalizador pode ser definido no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4830-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="c4830-166">No diretório raiz do aplicativo Web, ou seja, **d:\home\site\wwwroot**, crie um diretório **webapps** (se ainda não existir um) e coloque o Hudson.war em **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="c4830-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="c4830-167">Baixe o Apache Maven 3.0.5 (compatível com Hudson) e coloque-o em **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="c4830-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="c4830-168">Criar um Web. config em **d:\home\site\wwwroot** e colar Olá no seu conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4830-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="c4830-169">Neste ponto Olá web aplicativo pode ser reiniciado tootake Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="c4830-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="c4830-170">Conecte-se toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="c4830-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="c4830-171">Depois de Hudson configura a mesmo, você deverá ver Olá tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4830-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="c4830-173">Olá acesso página de configuração Hudson: clique em **Hudson gerenciar**e, em seguida, clique em **Configurar sistema**.</span><span class="sxs-lookup"><span data-stu-id="c4830-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="c4830-174">Configure Olá JDK, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4830-174">Configure hello JDK as shown below:</span></span>
   
    ![Configuração do Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="c4830-176">Configure o Maven conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4830-176">Configure Maven as shown below:</span></span>
   
    ![Configuração do Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="c4830-178">Salve configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4830-178">Save hello settings.</span></span> <span data-ttu-id="c4830-179">O Hudson agora deve estar configurado e pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="c4830-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="c4830-180">Para obter informações adicionais sobre o Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="c4830-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="c4830-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="c4830-181">Liferay</span></span>
<span data-ttu-id="c4830-182">O Liferay tem suporte em Aplicativos Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4830-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="c4830-183">Como Liferay pode exigir significativa da memória, Olá web aplicativo precisa toorun em um trabalho de dedicada médio ou grande, que pode fornecer memória suficiente.</span><span class="sxs-lookup"><span data-stu-id="c4830-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="c4830-184">Liferay também ocupa toostart de vários minutos.</span><span class="sxs-lookup"><span data-stu-id="c4830-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="c4830-185">Por esse motivo, é recomendável que você defina o aplicativo web de saudação muito**AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="c4830-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="c4830-186">Usando Liferay 6.1.2 que Community Edition GA3 fornecido com o Tomcat, hello arquivos a seguir foram editados depois de baixar Liferay:</span><span class="sxs-lookup"><span data-stu-id="c4830-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="c4830-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="c4830-187">**Server.xml**</span></span>

* <span data-ttu-id="c4830-188">Altere o desligamento porta muito-1.</span><span class="sxs-lookup"><span data-stu-id="c4830-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="c4830-189">Alterar também o conector HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="c4830-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="c4830-190">Comente o conector do hello AJP.</span><span class="sxs-lookup"><span data-stu-id="c4830-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="c4830-191">Em Olá **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** pasta, crie um arquivo chamado **ext.properties portal**.</span><span class="sxs-lookup"><span data-stu-id="c4830-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="c4830-192">Este arquivo deve toocontain uma linha, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="c4830-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="c4830-193">Em Olá o mesmo nível de diretório como pasta de 7.0.40 tomcat Olá, crie um arquivo chamado **Web. config** com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4830-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="c4830-194">Em Olá **httpPlatform** bloquear, hello **requestTimeout** está definido muito "00:10:00".</span><span class="sxs-lookup"><span data-stu-id="c4830-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="c4830-195">Ele pode ser reduzido mas, em seguida, você provavelmente toosee alguns erros de tempo limite durante a inicialização de Liferay.</span><span class="sxs-lookup"><span data-stu-id="c4830-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="c4830-196">Se esse valor for alterado, Olá **connectionTimeout** no tomcat Olá XML também deve ser modificado.</span><span class="sxs-lookup"><span data-stu-id="c4830-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="c4830-197">Vale a pena observar que varariable de ambiente Olá JRE_HOME é especificado em Olá acima Web. config toopoint toohello JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="c4830-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="c4830-198">padrão de saudação é de 32 bits, mas como Liferay pode exigir altos níveis de memória, é recomendável toouse Olá JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="c4830-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="c4830-199">Depois de fazer essas alterações, reinicie o aplicativo Web executando o Liferay. Em seguida, abra http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="c4830-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="c4830-200">portal de Liferay de saudação está disponível na raiz do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="c4830-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4830-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4830-201">Next steps</span></span>
<span data-ttu-id="c4830-202">Para obter mais informações sobre o Liferay, consulte [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="c4830-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="c4830-203">Para obter mais informações sobre o Java, consulte [Azure para desenvolvedores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="c4830-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[do serviço de aplicativo do Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
