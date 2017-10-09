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
# <a name="upload-a-custom-java-web-app-tooazure"></a>Carregar um tooAzure de aplicativo de web Java personalizado
Este tópico explica como um Java personalizados de tooupload web aplicativo muito[do serviço de aplicativo do Azure] aplicativos Web. Há informações que se aplicam a tooany site de Java ou aplicativo web e também alguns exemplos de aplicativos específicos.

Observe que o Azure fornece um meio para a criação de aplicativos da web de Java usando a interface de configuração do Portal do Azure hello e hello Azure Marketplace, conforme documentado em [criar um aplicativo da web de Java no serviço de aplicativo do Azure](web-sites-java-get-started.md). Este tutorial destina-se a cenários em que você não deseja toouse hello Azure Portal configuração da interface do usuário ou hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Diretrizes de configuração
a seguir Olá descreve configurações de Olá esperadas para aplicativos de web Java personalizados no Azure.

* porta HTTP de saudação usada pelo Olá processo Java é atribuída dinamicamente.  processo de saudação deve usar a porta de saudação da variável de ambiente Olá `HTTP_PLATFORM_PORT`.
* Todos os escutam portas diferente de ouvinte HTTP única de saudação deve ser desabilitado.  No Tomcat, que inclui o desligamento hello, HTTPS e AJP portas.
* contêiner de saudação deve toobe configurado para somente ao tráfego IPv4.
* Olá **inicialização** de comando para o aplicativo hello precisa toobe definidas na configuração de saudação.
* Aplicativos que exigem a permissão de gravação de diretórios com precisam toobe localizado no diretório de conteúdo do aplicativo da web do Azure hello, que é **d:\home.**.  variável de ambiente Olá `HOME` refere-se tooD:\home.  

Você pode definir variáveis de ambiente conforme necessário no arquivo Web. config de saudação.

## <a name="webconfig-httpplatform-configuration"></a>Configuração de httpPlatform do web.config
Olá, informações a seguir descrevem Olá **httpPlatform** formato em Web. config.

**arguments** (Padrão=""). Argumentos toohello executável ou script especificado na Olá **processPath** configuração.

Exemplos (mostrados com **processPath** incluído):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello de caminho executável ou script que irá iniciar um processo que escuta solicitações HTTP.

Exemplos:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (Padrão = 10.) Número de vezes que o processo de saudação especificado no **processPath** é permitido toocrash por minuto. Se esse limite for excedido, **HttpPlatformHandler** interromperá a inicialização do processo Olá restante Olá minuto hello.

**requestTimeout** (Padrão="00:02:00".) Duração para a qual **HttpPlatformHandler** esperará por uma resposta do processo de saudação escutando `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (Padrão = 10.) Número de vezes **HttpPlatformHandler** tentará o processo de saudação toolaunch especificado no **processPath**. Confira **startupTimeLimit** para obter mais detalhes.

**startupTimeLimit** (Padrão = 10 segundos.) Duração para a qual **HttpPlatformHandler** aguardará Olá executável/script toostart um processo que escuta na porta hello.  Se esse tempo limite for excedido, **HttpPlatformHandler** irá interromper o processo de saudação e tente toolaunch novamente **startupRetryCount** vezes.

**stdoutLogEnabled** (Padrão = "true".) Se true, **stdout** e **stderr** processo Olá especificado no hello **processPath** configuração será redirecionado toohello arquivo especificado no  **stdoutLogFile** (consulte **stdoutLogFile** seção).

**stdoutLogFile** (Padrão="d:\home\LogFiles\httpPlatformStdout.log".) Caminho de arquivo absoluto para o qual **stdout** e **stderr** do processo de saudação especificado em **processPath** será registrado.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`é um espaço reservado especial que deve toospecified como parte de **argumentos** ou como parte da saudação **httpPlatform** **environmentVariables** lista. Isso será substituído por uma porta gerada internamente pelo **HttpPlatformHandler** para que o processo de saudação especificado por **processPath** pode escutar nesta porta.
> 
> 

## <a name="deployment"></a>Implantação
Os aplicativos web Java com base podem ser implantados facilmente na maior parte do hello que mesmo significa que é usados com aplicativos de web de serviços de informações da Internet (IIS) com base em hello.  FTP, Git e Kudu é todos suportado como mecanismos de implantação, conforme é Olá recurso SCM integrado para aplicativos web. O WebDeploy funciona como um protocolo, no entanto, como o Java não é desenvolvido no Visual Studio, o WebDeploy não é adequado para casos de uso de implantação de aplicativos Web Java.

## <a name="application-configuration-examples"></a>Exemplos de configuração de aplicativos
Para Olá a seguir de aplicativos, um arquivo Web. config e hello configuração de aplicativo é fornecida como exemplos tooshow como tooenable seu aplicativo Java em aplicativos de Web do serviço de aplicativo.

### <a name="tomcat"></a>Tomcat
Existem duas variações no Tomcat que são fornecidas com o serviço de aplicativo Web de aplicativos, ainda é instâncias específicas do cliente tooupload bem possível. A seguir, um exemplo de uma instalação do Tomcat com uma JVM (Máquina Virtual Java) diferente.

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

Em Olá lado Tomcat, há algumas alterações de configuração que precisam toobe feita. Olá XML precisa tooset toobe editado:

* Shutdown port = -1
* HTTP connector port = ${port.http}
* HTTP connector address = "127.0.0.1"
* Comente os conectores HTTPS e AJP
* configuração de IPv4 saudação também pode ser definida no arquivo Catalina de saudação onde você pode adicionar`java.net.preferIPv4Stack=true`

Chamadas de Direct3d não têm suporte em Aplicativos Web do Serviço de Aplicativo. toodisable, adicione Olá seguinte opção Java deve seu aplicativo fazer essas chamadas:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Como é o caso de Olá para Tomcat, os clientes podem carregar suas próprias instâncias para Jetty. No caso de saudação de execução instalação completa de saudação do Jetty, configuração de saudação teria esta aparência:

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

configuração do Jetty Hello precisa toobe alterado em Olá start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
Em ordem tooget um Springboot aplicativo em execução, você precisa tooupload seu arquivo JAR ou WAR e adicione Olá após o arquivo Web. config. arquivo Web. config de saudação se encaixa na pasta wwwroot hello. No Web. config de saudação ajustar o arquivo JAR do hello argumentos toopoint tooyour, no hello seguir o arquivo JAR do exemplo hello está localizado em Olá na pasta wwwroot também.  

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


### <a name="hudson"></a>Hudson
Nosso teste usado Olá war Hudson 3.1.2 e Olá a instância padrão do Tomcat 7.0.50, mas sem usando coisas que tooset Olá da interface do usuário.  Como Hudson é uma ferramenta de compilação do software, é aconselhável tooinstall-la no dedicado instâncias onde hello **AlwaysOn** sinalizador pode ser definido no aplicativo web de saudação.

1. No diretório raiz do aplicativo Web, ou seja, **d:\home\site\wwwroot**, crie um diretório **webapps** (se ainda não existir um) e coloque o Hudson.war em **d:\home\site\wwwroot\webapps**.
2. Baixe o Apache Maven 3.0.5 (compatível com Hudson) e coloque-o em **d:\home\site\wwwroot**.
3. Criar um Web. config em **d:\home\site\wwwroot** e colar Olá no seu conteúdo a seguir:
   
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
   
    Neste ponto Olá web aplicativo pode ser reiniciado tootake Olá alterações.  Conecte-se toohttp://yourwebapp/hudson toostart Hudson.
4. Depois de Hudson configura a mesmo, você deverá ver Olá tela a seguir:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Olá acesso página de configuração Hudson: clique em **Hudson gerenciar**e, em seguida, clique em **Configurar sistema**.
6. Configure Olá JDK, conforme mostrado abaixo:
   
    ![Configuração do Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Configure o Maven conforme mostrado abaixo:
   
    ![Configuração do Maven](./media/web-sites-java-custom-upload/maven.png)
8. Salve configurações de saudação. O Hudson agora deve estar configurado e pronto para uso.

Para obter informações adicionais sobre o Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
O Liferay tem suporte em Aplicativos Web do Serviço de Aplicativo. Como Liferay pode exigir significativa da memória, Olá web aplicativo precisa toorun em um trabalho de dedicada médio ou grande, que pode fornecer memória suficiente. Liferay também ocupa toostart de vários minutos. Por esse motivo, é recomendável que você defina o aplicativo web de saudação muito**AlwaysOn**.  

Usando Liferay 6.1.2 que Community Edition GA3 fornecido com o Tomcat, hello arquivos a seguir foram editados depois de baixar Liferay:

**Server.xml**

* Altere o desligamento porta muito-1.
* Alterar também o conector HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Comente o conector do hello AJP.

Em Olá **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** pasta, crie um arquivo chamado **ext.properties portal**. Este arquivo deve toocontain uma linha, conforme mostrado aqui:

    liferay.home=%HOME%/site/wwwroot/liferay

Em Olá o mesmo nível de diretório como pasta de 7.0.40 tomcat Olá, crie um arquivo chamado **Web. config** com hello conteúdo a seguir:

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

Em Olá **httpPlatform** bloquear, hello **requestTimeout** está definido muito "00:10:00".  Ele pode ser reduzido mas, em seguida, você provavelmente toosee alguns erros de tempo limite durante a inicialização de Liferay.  Se esse valor for alterado, Olá **connectionTimeout** no tomcat Olá XML também deve ser modificado.  

Vale a pena observar que varariable de ambiente Olá JRE_HOME é especificado em Olá acima Web. config toopoint toohello JDK de 64 bits. padrão de saudação é de 32 bits, mas como Liferay pode exigir altos níveis de memória, é recomendável toouse Olá JDK de 64 bits.

Depois de fazer essas alterações, reinicie o aplicativo Web executando o Liferay. Em seguida, abra http://yourwebapp. portal de Liferay de saudação está disponível na raiz do aplicativo web hello. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o Liferay, consulte [http://www.liferay.com](http://www.liferay.com).

Para obter mais informações sobre o Java, consulte [Azure para desenvolvedores Java](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[do serviço de aplicativo do Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
