---
title: "aaaCreate um aplicativo Web no serviço de aplicativo do Azure usando Olá SDK do Azure para Java"
description: "Saiba como toocreate um aplicativo Web no serviço de aplicativo do Azure programaticamente usando Olá SDK do Azure para Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Criar um aplicativo Web no serviço de aplicativo do Azure usando Olá SDK do Azure para Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Visão geral
Este passo a passo mostra como toocreate um SDK do Azure para um aplicativo Java que cria um aplicativo Web no [do serviço de aplicativo do Azure][Azure App Service], em seguida, implantar um aplicativo tooit. Ele consiste em duas partes:

* Parte 1 demonstra como toobuild um aplicativo Java que cria um aplicativo web.
* Parte 2 demonstra como toocreate um JSP simple "Alô mundo" aplicativo, em seguida, use um FTP cliente toodeploy código tooApp serviço.

## <a name="prerequisites"></a>Pré-requisitos
### <a name="software-installations"></a>Instalações de software
Olá AzureWebDemo código do aplicativo neste artigo foi escrito usando o Azure Java SDK 0.7.0, que pode ser instalado usando Olá [Web Platform Installer] [ Web Platform Installer] (WebPI). Além disso, certifique-se de que toouse Olá última versão do hello [Kit de ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]. Depois de instalar o SDK de hello, atualizar dependências Olá em seu projeto Eclipse executando **Atualizar índice** na **Maven repositórios**, adicionar novamente a versão mais recente de saudação de cada pacote hello  **Dependências** janela. Você pode verificar a versão de saudação do software instalado no Eclipse, clicando em **Ajuda > detalhes da instalação**; você deve ter pelo menos Olá seguintes versões:

* Pacote para Bibliotecas do Microsoft Azure para Java 0.7.0.20150309
* Eclipse IDE para desenvolvedores de Java EE 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Criar e configurar recursos de nuvem no Azure
Antes de iniciar este procedimento, você precisa toohave uma assinatura ativa do Azure e configurar um padrão de AD (Active Directory) no Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Criar um AD (Active Directory) no Azure
Se você não tiver um Active Directory (AD) em sua assinatura do Azure, faça logon no hello [portal clássico do Azure] [ Azure classic portal] com sua conta da Microsoft. Se você tiver várias assinaturas, clique em **assinaturas** e selecione saudação padrão diretório para assinatura Olá deseja toouse para este projeto. Em seguida, clique em **aplicar** tooswitch toothat exibição da assinatura.

1. Selecione **do Active Directory** no menu de saudação à esquerda. **Clique em Novo > Diretório > Criação Personalizada**.
2. Em **Adicionar Diretório**, selecione **Criar Novo Diretório**.
3. Em **Nome**, insira um nome de diretório.
4. Em **Domínio**, insira um nome de domínio. Este é um nome de domínio básico que está incluído por padrão com seu diretório; ele tem o formato de saudação `<domain_name>.onmicrosoft.com`. Você pode nomear com base no nome do diretório hello ou outro nome de domínio que você possui. Posteriormente, você pode adicionar outro nome de domínio que sua organização já utilize.
5. Em **País ou região**, selecione sua localidade.

Para saber mais sobre o AD, confira [O que é um diretório do Azure AD][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Criar um Certificado de Gerenciamento do Azure
Olá SDK do Azure para Java usa tooauthenticate de certificados de gerenciamento com assinaturas do Azure. Esses são x. 509 v3 certificados que usar tooauthenticate um aplicativo cliente que usa Olá tooact de API de gerenciamento de serviços em nome de recursos de assinatura toomanage do proprietário de assinatura de saudação.

código de Olá neste procedimento usa um certificado autoassinado tooauthenticate com o Azure. Para esse procedimento, você precisa toocreate um certificado e carregá-lo toohello [portal clássico do Azure] [ Azure classic portal] com antecedência. Isso envolve Olá etapas a seguir:

* Gere um arquivo PFX que represente seu certificado de cliente e salve-o localmente.
* Gere um certificado de gerenciamento (arquivo CER) do arquivo PFX de saudação.
* Carregar Olá CER arquivo tooyour assinatura do Azure.
* Converta o arquivo PFX de saudação em JKS, como Java usa esse tooauthenticate formato usando certificados.
* Grave o código de autenticação do aplicativo hello, que se refere a arquivos JKS local toohello.

Quando você concluir este procedimento, certificado CER Olá residem em sua assinatura do Azure e certificado JKS Olá residem em sua unidade local. Para saber mais sobre gerenciamento de certificados, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Criar um certificado
toocreate seu próprio certificado autoassinado, abra um console de comando em seu sistema operacional e execute Olá comandos a seguir.

> **Observação:** computador Olá no qual você executa este comando deve ter Olá JDK instalado. Além disso, Olá caminho toohello keytool depende local Olá em que você instala Olá JDK. Para obter mais informações, consulte [chave e a ferramenta de gerenciamento de certificado (keytool)] [ Key and Certificate Management Tool (keytool)] em documentos online do hello Java.
> 
> 

arquivo do toocreate hello. pfx:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

arquivo. cer Olá toocreate:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

onde:

* `<java-install-dir>`é Olá caminho toohello diretório no qual você instalou o Java.
* `<keystore-id>`é o identificador de entrada de repositório de chaves de saudação (por exemplo, `AzureRemoteAccess`).
* `<cert-store-dir>`é Olá caminho toohello diretório no qual você deseja toostore certificados (por exemplo `C:/Certificates`).
* `<cert-file-name>`é o nome Olá Olá do arquivo de certificado (por exemplo `AzureWebDemoCert`).
* `<password>`senha Olá escolher certificado de saudação tooprotect; ele deve ter pelo menos 6 caracteres. Embora isso não seja recomendado, você optar por não inserir nenhuma senha.
* `<dname>`é Olá nome diferenciado do x. 500 toobe associada alias e é usado como o emissor hello e campos de entidade no certificado autoassinado hello.

Para saber mais, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Carregar certificado Olá
tooupload tooAzure um certificado autoassinado, vá toohello **configurações** página no portal clássico do hello, clique em Olá **certificados de gerenciamento** guia. Clique em **carregar** final Olá Olá página e navegar toohello local do arquivo CER Olá que você criou.

#### <a name="convert-hello-pfx-file-into-jks"></a>Converter o arquivo PFX de saudação em JKS
Saudação de Prompt de comando do Windows (executando como administrador), cd toohello diretório que contém Olá certificados e executado Olá a seguir de comando, onde `<java-install-dir>` é Olá diretório no qual você instalou Java em seu computador:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Quando solicitado, insira a senha de chave de armazenamento de destino Olá; Essa será a senha Olá para o arquivo JKS hello.
2. Quando solicitado, insira a senha de chave de armazenamento de origem Olá; Esta é Olá senha especificada para o arquivo PFX de saudação.

as duas senhas de saudação não tem toobe Olá mesmo. Embora isso não seja recomendado, você optar por não inserir nenhuma senha.

## <a name="build-a-web-app-creation-application"></a>Compilar um aplicativo de criação de aplicativos Web
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Criar hello espaço de trabalho do Eclipse e projeto Maven
Nesta seção, você criará um espaço de trabalho e um projeto Maven para o aplicativo para criação de aplicativos do web hello, denominado AzureWebDemo.

1. Crie um novo projeto Maven. Clique em **Arquivo > Novo > Projeto Maven**. Em **Novo Projeto Maven**, selecione **Criar um projeto simples** e **Usar local padrão de espaço de trabalho**.
2. Na segunda página de saudação do **novo projeto Maven**, especifique Olá seguinte:
   
   * ID do Grupo: `com.<username>.azure.webdemo`
   * ID do Artefato: AzureWebDemo
   * Versão: 0.0.1-SNAPSHOT
   * Empacotamento: jar
   * Nome: AzureWebDemo
     
     Clique em **Concluir**.
3. Abra o arquivo de pom.xml de saudação do novo projeto no Explorador de projeto. Selecione Olá **dependências** guia. Já que esse é um novo projeto, nenhum pacote está listado ainda.
4. Exibir hello abrir Maven repositórios. **Clique em Janela > Mostrar Exibição > Outros > Maven > Repositórios Maven** e clique em **OK**. Olá **Maven repositórios** exibição aparecerá na parte inferior de saudação do hello IDE.
5. Abra **repositórios Global**, Olá do botão direito do mouse **central** repositório e selecione **recriar índice**.
   
    ![][1]
   
    Esta etapa pode levar vários minutos dependendo da velocidade da saudação de sua conexão. Quando recriações de índice hello, você verá pacotes Microsoft Azure Olá Olá **central** Repositório Maven.
6. Em **Dependências**, clique em **Adicionar**. Em **Inserir ID do Grupo...**, digite `azure-management`. Selecione os pacotes de saudação para gerenciamento de base e o gerenciamento de serviço de aplicativo Web de aplicativos:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Observação:** se você estiver atualizando dependências Olá após uma nova versão, você precisa toore-adicionar cada uma das dependências de saudação nesta lista.
   > Depois de clicar em **adicionar** e selecione cada dependência, ela será exibida com o novo número de versão Olá no hello **dependências** lista.
   > 
   > 

Clique em **OK**. Olá pacotes do Azure e aparecem em Olá **dependências** lista.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Escrevendo código Java tooCreate um aplicativo Web por saudação da chamada do SDK do Azure
Em seguida, escreva um código de saudação que chama as APIs no SDK do Azure de saudação de saudação do Java toocreate aplicativo do serviço de aplicativo web.

1. Crie um código de ponto de entrada principal Java classe toocontain hello. No Explorador de projeto, clique com botão direito no nó do projeto hello e selecione **Novo > classe**.
2. Em **nova classe Java**, nomeie a classe Olá `WebCreator` e verifique Olá **público estático anulado main** caixa de seleção. seleções de saudação devem aparecer da seguinte maneira:
   
    ![][2]
3. Clique em **Concluir**. arquivo de WebCreator.java Olá aparece no Explorador de projeto.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Olá tooCreate de API do Azure ao chamar um serviço de aplicativo de um aplicativo Web
#### <a name="add-necessary-imports"></a>Adicionar as importações necessárias
Em WebCreator.java, adicione Olá a seguir importa; Esses importações fornecem acesso tooclasses em Olá bibliotecas de gerenciamento para o consumo de APIs do Azure:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>Definir a classe de ponto de entrada principal Olá
Como objetivo Olá Olá AzureWebDemo aplicativo é toocreate um serviço de aplicativo de um aplicativo Web, nome de classe principal Olá para este aplicativo `WebAppCreator`. Essa classe fornece código de ponto de entrada principal Olá que chama Olá API de gerenciamento de serviços do Azure toocreate Olá web app.

Adicione Olá definições de parâmetro para Olá web app e o espaço da Web a seguir. Você precisará tooprovide suas próprias informações de ID e o certificado de assinatura do Azure.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

onde:

* `<subscription-id>`é Olá ID de assinatura do Azure no qual você deseja que o recurso de saudação toocreate.
* `<certificate-store-path>`é Olá caminho e nome de arquivo toohello JKS arquivo em seu diretório de repositório de certificados local. Por exemplo, `C:/Certificates/CertificateName.jks` para Linux e `C:\Certificates\CertificateName.jks` para Windows.
* `<certificate-password>`é a senha de saudação que você especificou quando criou seu certificado JKS.
* `webAppName`pode ser qualquer nome que você escolher; Este procedimento usa o nome da saudação `WebDemoWebApp`. o nome de domínio completo Olá é hello `webAppName` com hello `domainName` anexado, portanto nesse caso domínio completo Olá é `webdemowebapp.azurewebsites.net`.
* `domainName` deve ser especificado conforme mostrado acima.
* `webSpaceName`deve ser um dos valores de saudação definidos no hello [WebSpaceNames] [ WebSpaceNames] classe.
* `appServicePlanName` deve ser especificado conforme mostrado acima.

> **Observação:** sempre executar este aplicativo, você precisa toochange Olá valor de `webAppName` e `appServicePlanName` (ou excluir Olá web app no hello Portal do Azure) antes de executar o aplicativo hello novamente. Caso contrário, a execução falhará porque hello mesmo recurso já existe no Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Definir o método de criação de web hello
Em seguida, defina um aplicativo web do método toocreate hello. Esse método, `createWebApp`, especifica os parâmetros de saudação do Olá web app e Olá espaço na Web. Ele também cria e configura o cliente de gerenciamento de aplicativos de Web do serviço de aplicativo hello, que é definido como Olá [WebSiteManagementClient] [ WebSiteManagementClient] objeto. cliente de gerenciamento de saudação é chave toocreating os aplicativos Web. Ele fornece os serviços web RESTful que permitem que aplicativos toomanage aplicativos web (executando operações como criar, atualizar e excluir) ao chamar a API de gerenciamento do serviço de saudação.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

código de Olá mostrará o status HTTP de saudação da resposta Olá indicando êxito ou falha e se for bem-sucedido, produzirá o nome de saudação do hello criado o aplicativo web.

#### <a name="define-hello-main-method"></a>Definir o método Main () de saudação
Fornece o código do método Main Olá esse aplicativo de web chamadas createWebApp() toocreate Olá.

Finalmente, chame `createWebApp` em `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Executar o aplicativo hello e verifique se a criação do aplicativo web
tooverify que seu aplicativo é executado, clique em **Executar > executar**. Quando o aplicativo hello conclui a execução, você deve ver Olá saída no console do Eclipse Olá a seguir:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Faça logon no portal clássico do Azure de saudação e clique em **aplicativos Web**. novo aplicativo web e Olá deve aparecer na lista de aplicativos Web hello dentro de alguns minutos.

## <a name="deploying-an-application-toohello-web-app"></a>Implantando um aplicativo Web de toohello do aplicativo
Depois que você executou AzureWebDemo e criou um novo aplicativo de web hello, faça logon no portal clássico do hello, clique em **aplicativos Web**e selecione **WebDemoWebApp** em Olá **aplicativos Web** lista. Na página do painel do aplicativo da web hello, clique em **procurar** (ou clique em URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Você verá uma página de espaço reservado em branco, porque nenhum conteúdo foi publicado toohello web aplicativo ainda.

Em seguida você criará um aplicativo "Hello World" e implantá-lo toohello web app.

### <a name="create-a-jsp-hello-world-application"></a>Criar um aplicativo Olá Mundo
#### <a name="create-hello-application"></a>Criar um aplicativo hello
Em ordem toodemonstrate como toodeploy web de toohello um aplicativo, Olá procedimento a seguir mostra como toocreate um aplicativo "Hello World" Java simples e carregá-lo toohello aplicativo serviço Web de aplicativo que criou seu aplicativo.

1. Clique em **Arquivo > Novo > Projeto Web Dinâmico**. Nomeie-o `JSPHello`. Não é necessário toochange outras configurações nesta caixa de diálogo. Clique em **Concluir**.
   
    ![][3]
2. No Explorador de projeto, expanda Olá **JSPHello** de projeto, clique no **WebContent**, em seguida, clique em **Novo > arquivo JSP**. Na caixa de diálogo de novo arquivo JSP hello, nomeie o novo arquivo de saudação `index.jsp`. Clique em **Avançar**.
3. Em Olá **Selecionar modelo JSP** caixa de diálogo, selecione **novo arquivo JSP (html)** e clique em **concluir**.
4. No index.jsp, adicione Olá Olá código a seguir `<head>` e `<body>` marca seções:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Executar o aplicativo hello World Olá no localhost
Antes de executar este aplicativo, você precisa tooconfigure algumas propriedades.

1. Saudação de atalho **JSPHello** do projeto e selecione **propriedades**.
2. Em hello **propriedades** caixa de diálogo: selecione **caminho de compilação de Java**, selecione Olá **ordenar e exportar** guia, verifique **JRE biblioteca do sistema**, em seguida, clique em **Backup** toomove-toohello superior da lista de saudação.
   
    ![][4]
3. Também no hello **propriedades** caixa de diálogo: selecione **tempos de execução de destino** e clique em **novo**.
4. Em Olá **novo ambiente de tempo de execução do servidor** caixa de diálogo, selecione um servidor, como **versão 7.0 do Apache Tomcat** e clique em **próximo**. Em Olá **servidor Tomcat** caixa de diálogo, defina **nome** muito`Apache Tomcat v7.0`e defina **diretório de instalação do Tomcat** toohello diretório no qual você instalou a versão de saudação do Servidor Tomcat toouse desejado.
   
    ![][5]
   
    Clique em **Concluir**.
5. Você, em seguida, retornar toohello **tempos de execução de destino** página de saudação **propriedades** caixa de diálogo. Selecione **Apache Tomcat v7.0** e clique em **OK**.
   
    ![][6]
6. Em Olá Eclipse **executar** menu, clique em **executar**. Em Olá **executar como** caixa de diálogo, selecione **executado no servidor**. Em Olá **executado no servidor** caixa de diálogo, selecione **Tomcat v 7.0 Server**:
   
    ![][7]
   
    Clique em **Concluir**.
7. Olá quando o aplicativo é executado, você deve ver Olá **JSPHello** página exibida em uma janela de localhost no Eclipse (`http://localhost:8080/JSPHello/`), exibindo Olá a seguinte mensagem de erro:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Exportar aplicativo hello como um WAR
Exporte arquivos de projeto web hello como um arquivo da web (WAR) para que você possa implantar aplicativo da web de toohello. Olá seguintes arquivos de projeto web residem na pasta de conteúdo da Web hello:

    META-INF
    WEB-INF
    index.jsp

1. Pasta de conteúdo da Web hello e selecione **exportar**.
2. Em Olá **exportar selecione** caixa de diálogo, clique em **Web > WAR** arquivo e, em seguida, clique em **próximo**.
3. Em Olá **WAR exportar** caixa de diálogo, selecione diretório src de saudação no projeto atual Olá e incluir nome de Olá de arquivo WAR de saudação final hello. Por exemplo:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Para obter mais informações sobre como implantar arquivos WAR, consulte [adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Implantando Olá Olá mundo de aplicativos usando o FTP
Selecione um aplicativo de terceiros FTP cliente toopublish hello. Este procedimento descreve duas opções: console de Kudu Olá embutido no Azure. e FileZilla, uma ferramenta popular com uma interface do usuário gráfica, conveniente.

> **Observação:** Olá Kit de ferramentas do Azure para Eclipse dá suporte a contas de toostorage de implantação e a nuvem de serviços, mas não oferece suporte a aplicativos de tooweb de implantação. Você pode implantar toostorage contas e serviços usando um projeto de implantação do Azure conforme descrito em nuvem [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mas não tooweb aplicativos. Use outros métodos como FTP ou GitHub tootransfer arquivos tooyour web app.
> 
> **Observação:** não recomendamos o uso de FTP do prompt de comando do Windows hello (Olá de linha de comando FTP.EXE utilitário fornecido com o Windows). Clientes FTP que usam o FTP ativo, como FTP.EXE, geralmente failover toowork firewalls. FTP ativo Especifica um endereço interno da rede local, servidor toowhich um FTP provavelmente falharão tooconnect.
> 
> 

Para obter mais informações sobre o aplicativo de implantação tooan do serviço de aplicativo web usando FTP, consulte Olá seguintes tópicos:

* [Implantar usando um utilitário FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Configurar credenciais de implantação
Verifique se você executou Olá **AzureWebDemo** toocreate aplicativo um aplicativo web. Você transferirá toothis local dos arquivos.

1. Faça logon no portal clássico do hello e clique em **aplicativos Web**. Certifique-se de **WebDemoWebApp** aparece na lista de saudação de aplicativos web e certifique-se de que ele está em execução. Clique em **WebDemoWebApp** tooopen sua **painel** página.
2. Em Olá **painel** página em **rápidos**, clique em **configurar suas credenciais de implantação** (se você já tiver credenciais de implantação, lê  **Redefinir as credenciais de implantação**).
   
    As credenciais de implantação estão associadas com uma conta da Microsoft. Você precisa toospecify um nome de usuário e senha que você pode usar toodeploy usando Git e FTP. Você pode usar essas credenciais toodeploy tooany web app em todas as assinaturas do Azure associadas à sua conta da Microsoft. Forneça credenciais de implantação do Git e FTP na caixa de diálogo Olá e saudação de registro de nome de usuário e senha para uso futuro.

#### <a name="get-ftp-connection-information"></a>Obter informações de conexão de FTP
toouse FTP toodeploy aplicativo arquivos toohello recém-criado web aplicativo precisar de informações de conexão tooobtain. Há duas maneiras de obter informações de conexão tooobtain. É uma maneira toovisit Olá web aplicativo **painel** página; hello outra forma é toodownload Olá web aplicativo o perfil de publicação. saudação de perfil de publicação é um arquivo XML que fornece informações como credenciais de logon e o nome de host do FTP para seus aplicativos web no serviço de aplicativo do Azure. Você pode usar o nome de usuário e senha toodeploy tooany aplicativo web em todas as assinaturas associadas à saudação conta do Azure, não apenas esse um.

informações de conexão tooobtain FTP na folha do aplicativo da web de saudação em Olá [Portal do Azure][Azure Portal]:

1. Em **Essentials**, localize e copie Olá **hostname de FTP**. Este é um URI semelhante muito`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. Em **Essentials**, localize e copie o **nome de usuário de implantação/FTP**. Isso terá o formato de saudação *webappname\deployment-username*; por exemplo `WebDemoWebApp\deployer77`.

perfil de publicação de informações de conexão de FTP tooobtain da saudação:

1. Na folha do seu aplicativo da web hello, clique em **obter perfil de publicação**. Isso baixará uma unidade de local de tooyour do arquivo. publishsettings.
2. Abra o arquivo. publishsettings de saudação em um editor de XML ou editor de texto e localize Olá `<publishProfile>` elemento que contém `publishMethod="FTP"`. Ele deve ter aparência Olá a seguir:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Observe a esse aplicativo web de saudação `publishProfile` configurações mapeiam toohello FileZilla Site Manager configurações da seguinte maneira:

* `publishUrl`é Olá igual **nome de host do FTP**, Olá valor definido em **Host**.
* `publishMethod="FTP"`significa que você definir **protocolo** muito**FTP - File Transfer Protocol**, e **criptografia** muito**usar FTP simples**.
* `userName`e `userPWD` são chaves para Olá reais valores de nome de usuário e senha especificados quando você redefine credenciais de implantação de saudação. `userName`é Olá igual **implantação / FTP usuário**. Eles mapeiam muito**usuário** e **senha** em FileZilla.
* `ftpPassiveMode="True"`significa que esse site Olá FTP usa transferência por FTP passiva; Selecione **passivo** em Olá **as configurações de transferência** guia.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Configurar o aplicativo Web de saudação toohost um aplicativo Java
Antes de publicar o aplicativo hello, é necessário toochange algumas definições de configuração para que hello aplicativo web pode hospedar um aplicativo Java.

1. No portal clássico do hello, vá do aplicativo da web toohello **painel** página e clique em **configurar**. Em Olá **configurar** especifique Olá configurações a seguir.
2. Em **versão do Java** saudação padrão é **Off**; selecione versão do Java Olá destinos seu aplicativo; por exemplo 1.7.0_51. Depois de fazer isso, verifique também **contêiner da Web** é definir a versão de tooa do servidor Tomcat.
3. Em **documentos padrão**, adicione JSP e movê-lo para cima toohello superior da lista de saudação. (o arquivo de padrão de saudação para aplicativos web é hostingstart.html.)
4. Clique em **Salvar**.

#### <a name="publish-your-application-using-kudu"></a>Publicar seu aplicativo usando Kudu
Aplicativo de hello toopublish unidirecional é Olá toouse que kudu depurar console incorporada do Azure. O kudu é conhecido toobe estável e consistente com o serviço de aplicativo Web de aplicativos e servidor Tomcat. Você acessar o console de saudação do aplicativo web de saudação navegando tooa URL de saudação formulário a seguir:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Para esse procedimento, o console de Kudu de saudação está localizado em Olá seguindo a URL; Procure toothis local:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. No menu superior do hello, selecione **Console depuração > CMD**.
3. Na linha de comando do console hello, navegue muito`/site/wwwroot` (ou clique em `site`, em seguida, `wwwroot` no modo de exibição de diretório de saudação na parte superior de saudação da página de saudação):
   
    `cd /site/wwwroot`
4. Depois de especificar a **Versão do Java**, o servidor Tomcat deve criar uma pasta webapps. Na linha de comando do console hello, navegar toohello webapps diretório:
   
    `mkdir webapps`
   
    `cd webapps`
5. Arraste JSPHello.war de `<project-path>/JSPHello/src/` e inseri-la em modo de exibição de diretório Kudu de saudação em `/site/wwwroot/webapps`. Não arraste-a área "Arraste aqui tooupload e zip" toohello, porque o Tomcat será descompacte-o.
   
   ![][8]

No primeiro JSPHello.war aparece na área de diretório de saudação por si só:

  ![][9]

Em um curto período de tempo (provavelmente menos de 5 minutos) servidor Tomcat serão descompactados arquivo WAR de saudação em um diretório JSPHello descompactado. Clique em toosee de diretório raiz Olá se JSP foi descompactado e copiados para esse local. Nesse caso, navegue toohello back webapps diretório toosee se Olá desempacotados JSPHello diretório foi criado. Se você não ver esses itens, aguarde e repita.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Publicar seu aplicativo usando o FileZilla (opcional)
Outra ferramenta que você pode usar o aplicativo de hello toopublish é FileZilla, um cliente FTP de terceiros popular com uma interface do usuário gráfica, conveniente. Você pode baixar e instalar o FileZilla de [http://filezilla-project.org/](http://filezilla-project.org/) se você ainda não o tiver. Para obter mais informações sobre como usar o cliente hello, consulte Olá [FileZilla documentação](https://wiki.filezilla-project.org/Documentation) e essa entrada de blog em [os clientes FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. No FileZilla, clique em **Arquivo > Gerenciador de Sites**.
2. Em Olá **Site Manager** caixa de diálogo, clique em **novo Site**. Um novo site FTP em branco aparecerá no **Selecionar entrada** solicitando que você tooprovide um nome. Para este procedimento, nomeie-o como `AzureWebDemo-FTP`.
   
    Em Olá **geral** especifique Olá configurações a seguir:
   
   * **Host:** Enter Olá **nome de Host do FTP** que você copiou do painel de saudação.
   * **Porta:** (deixe em branco, pois isso é uma transferência de passivo e servidor de saudação determinará Olá porta toouse.)
   * **Protocolo:** protocolo FTP
   * **Criptografia:** usar FTP simples
   * **Tipo de Logon:** normal
   * **Usuário:** Enter Olá implantação / FTP de usuário que você copiou do painel de saudação. Isso é Olá completo FTP nome de usuário, que tem o formato de saudação *webappname\username*.
   * **Senha:** digite a senha Olá especificado quando você define as credenciais de implantação de saudação.
     
     Em Olá **as configurações de transferência** guia, selecione **passivo**.
3. Clique em **Conectar**. Se for bem-sucedida, console da FileZilla exibirá um `Status: Connected` mensagem e emitir um `LIST` conteúdo do diretório Olá toolist de comando.
4. Em Olá **Local** reside do painel do site, diretório de origem Olá select no arquivo hello JSPHello.war; caminho Olá será a seguir toohello semelhante:
   
    `<project-path>/JSPHello/src/`
5. Em Olá **remoto** painel do site, a pasta de destino de saudação select. Você implantará Olá WAR arquivo toohello `webapps` diretório na raiz do aplicativo da web de saudação. Navegue muito`/site/wwwroot`, clique duas vezes em `wwwroot`e selecione **criar diretório**. Diretório de nome de saudação `webapps` e insira o diretório.
6. Transferir JSPHello.war muito`/site/wwwroot/webapps`. Selecione JSPHello.war no hello **Local** lista de arquivos, clique com botão direito nele e selecione **carregar**. Você deverá vê-lo aparecer em `/site/wwwroot/webapps`.
7. Depois de copiar o diretório de webapps toohello JSPHello.war, servidor Tomcat será automaticamente Descompacte (unzip) Olá arquivos contidos no arquivo WAR hello. Embora o servidor Tomcat começa desempacotar quase imediatamente, pode levar um longo tempo (possivelmente horas) para Olá arquivos tooappear no cliente FTP de saudação.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Executar o aplicativo hello World Olá em Olá Web App
1. Após Olá WAR arquivo carregado e verificado que o servidor Tomcat criou um desempacotados `JSPHello` diretório, procurar muito`http://webdemowebapp.azurewebsites.net/JSPHello` aplicativo hello de toorun.
   
   > **Observação:** se você clicar em **procurar** no portal clássico do hello, você pode obter, página da Web padrão do hello dizendo "Este aplicativo web de Java com base tem foi criado com êxito." Você pode ter toorefresh Olá página na saída do aplicativo hello ordem tooview em vez de página da Web padrão de saudação.
   > 
   > 
2. Quando o aplicativo hello é executado, você verá uma página da web com hello saída a seguir:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Limpar recursos do Azure
Este procedimento cria um aplicativo Web do Serviço de Aplicativo. Você será cobrado para o recurso de saudação desde que ele existe. A menos que você planeje toocontinue usando Olá web app para teste ou desenvolvimento, você deve considerar parando ou excluí-lo. Um aplicativo Web cuja execução foi interrompida ainda incorrerá em um pequeno encargo, mas você poderá reiniciá-lo a qualquer momento. Excluir um aplicativo web apaga todos os dados que você carregou tooit.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
