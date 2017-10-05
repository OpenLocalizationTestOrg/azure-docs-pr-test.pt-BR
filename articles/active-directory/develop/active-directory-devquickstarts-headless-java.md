---
title: "Introdução à linha de comando Java do Azure AD | Microsoft Docs"
description: "Como criar um aplicativo de linha de comando Java que conecta os usuários para acessar uma API."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="7d3d1-103">Usando um aplicativo de linha de comando Java para acessar uma API com o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d3d1-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7d3d1-104">O AD do Azure torna simples e direto terceirizar o gerenciamento da identidade de seu aplicativo Web, fornecendo uma única entrada e uma única saída com apenas algumas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="7d3d1-105">Em aplicativos Web do Java, você pode conseguir isso usando a implementação da Microsoft do ADAL4J voltado para a comunidade.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="7d3d1-106">Aqui usaremos o ADAL4J para:</span><span class="sxs-lookup"><span data-stu-id="7d3d1-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="7d3d1-107">Conectar o usuário ao aplicativo usando o Azure AD como o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="7d3d1-108">Exibir algumas informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-108">Display some information about the user.</span></span>
* <span data-ttu-id="7d3d1-109">Desconectar o usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-109">Sign the user out of the app.</span></span>

<span data-ttu-id="7d3d1-110">Para isso, você precisará:</span><span class="sxs-lookup"><span data-stu-id="7d3d1-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="7d3d1-111">Registrar um aplicativo com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7d3d1-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="7d3d1-112">Configure seu aplicativo para usar a biblioteca ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="7d3d1-113">Use a biblioteca ADAL4J para emitir solicitações de entrada e saída ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="7d3d1-114">Imprimir dados sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-114">Print out data about the user.</span></span>

<span data-ttu-id="7d3d1-115">Para começar, [baixe o esqueleto do aplicativo](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [baixe o exemplo concluído](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7d3d1-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="7d3d1-116">Você também precisará de um locatário do AD do Azure no qual registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="7d3d1-117">Se você ainda não tiver um locatário, [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7d3d1-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="7d3d1-118">1.  Registrar um aplicativo com o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d3d1-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="7d3d1-119">Para habilitar seu aplicativo a autenticar usuários, primeiro você precisará registrar um novo aplicativo em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="7d3d1-120">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d3d1-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7d3d1-121">Na barra superior, clique na sua conta e, na lista **Diretório**, escolha o locatário do Active Directory em que você deseja registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="7d3d1-122">Clique em **Mais Serviços** no painel de navegação à esquerda e escolha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7d3d1-123">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="7d3d1-124">Siga os prompts e crie um novo **Aplicativo Web e/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="7d3d1-125">O **nome** do aplicativo descreverá seu aplicativo para os usuários finais</span><span class="sxs-lookup"><span data-stu-id="7d3d1-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="7d3d1-126">A **URL de logon** é a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="7d3d1-127">O padrão do esqueleto é `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="7d3d1-128">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="7d3d1-129">Você precisará desse valor nas próximas seções, portanto, copie-o da guia do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="7d3d1-130">Na página **Configurações** -> **Propriedades** do aplicativo, atualize o URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="7d3d1-131">O **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="7d3d1-132">A convenção é usar `https://<tenant-domain>/<app-name>`, por exemplo, `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="7d3d1-133">Quando estiver no portal de seu aplicativo, crie uma **Chave** na página **Configurações** para seu aplicativo e copie-a.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="7d3d1-134">Você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="7d3d1-135">2. Configurar seu aplicativo para usar a biblioteca ADAL4J e pré-requisitos para o uso do Maven</span><span class="sxs-lookup"><span data-stu-id="7d3d1-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="7d3d1-136">Aqui, configuraremos o ADAL4J para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="7d3d1-137">O ADAL4J será usado para emitir solicitações de entrada e saída, gerenciar a sessão do usuário e obter informações sobre o usuário, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="7d3d1-138">No diretório raiz do projeto, abra/crie `pom.xml`, localize o `// TODO: provide dependencies for Maven` e substitua-o pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="7d3d1-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="7d3d1-139">3. Criar o arquivo PublicClient Java</span><span class="sxs-lookup"><span data-stu-id="7d3d1-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="7d3d1-140">Conforme indicado acima, usaremos a Graph API para obter dados sobre o usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="7d3d1-141">Para que isso seja fácil, devemos criar um arquivo para representar um **Objeto de Diretório** e um arquivo individual para representar o **Usuário**, para que o padrão OO do Java possa ser usado.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="7d3d1-142">Crie um arquivo chamado `DirectoryObject.java` , que usaremos para armazenar os dados básicos sobre qualquer DirectoryObject (fique a vontade para usá-lo posteriormente para qualquer outra Consulta de Gráfico que você possa fazer).</span><span class="sxs-lookup"><span data-stu-id="7d3d1-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="7d3d1-143">Você pode recortar/colar isso abaixo:</span><span class="sxs-lookup"><span data-stu-id="7d3d1-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="7d3d1-144">Compilar e executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="7d3d1-144">Compile and run the sample</span></span>
<span data-ttu-id="7d3d1-145">Volte para seu diretório raiz e execute o comando a seguir para compilar o exemplo que você acabou de montar usando o `maven`.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="7d3d1-146">Isso usará o arquivo `pom.xml` que você escreveu para as dependências de arquivo.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="7d3d1-147">Agora você deve ter um arquivo `adal4jsample.war` em seu diretório do `/targets`.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="7d3d1-148">Você pode implantá-lo em seu contêiner do Tomcat e visitar a URL</span><span class="sxs-lookup"><span data-stu-id="7d3d1-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="7d3d1-149">É muito fácil de implantar um WAR com os servidores do Tomcat mais recentes.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="7d3d1-150">Basta navegar até `http://localhost:8080/manager/` e seguir as instruções sobre como carregar o arquivo ``adal4jsample.war\`.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="7d3d1-151">Ele será implantado automático com o ponto de extremidade correto.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7d3d1-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d3d1-152">Next Steps</span></span>
<span data-ttu-id="7d3d1-153">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="7d3d1-153">Congratulations!</span></span> <span data-ttu-id="7d3d1-154">Agora você tem um aplicativo Java com a capacidade de autenticar usuários, chamar APIs da Web com segurança usando OAuth 2.0 e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="7d3d1-155">Se você ainda não fez isso, agora é o momento de preencher seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="7d3d1-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="7d3d1-156">Para referência, o exemplo concluído (sem os valores de configuração) [é fornecido como um .zip aqui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="7d3d1-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

