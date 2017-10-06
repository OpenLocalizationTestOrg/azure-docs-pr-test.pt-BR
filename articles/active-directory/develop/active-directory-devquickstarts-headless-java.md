---
title: "aaaAzure linha de comando do AD Java Introdução | Microsoft Docs"
description: "Como toobuild um Java comando aplicativo de linha que conecta os usuários tooaccess uma API."
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
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="78086-103">Usando o aplicativo de linha de comando do Java tooAccess uma API com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="78086-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="78086-104">O AD do Azure torna simple e direto toooutsource gerenciamento de identidade do seu aplicativo web, fornecendo a única entrada e saída com apenas algumas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="78086-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="78086-105">Em aplicativos da web de Java, você pode fazer isso usando a implementação da Microsoft da saudação ADAL4J dirigida pela comunidade.</span><span class="sxs-lookup"><span data-stu-id="78086-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="78086-106">Aqui usaremos o ADAL4J para:</span><span class="sxs-lookup"><span data-stu-id="78086-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="78086-107">Entrada hello usuário no aplicativo hello usando o Azure AD como provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="78086-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="78086-108">Exiba algumas informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="78086-108">Display some information about hello user.</span></span>
* <span data-ttu-id="78086-109">Entrada hello usuário fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="78086-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="78086-110">Em ordem toodo isso, você precisará:</span><span class="sxs-lookup"><span data-stu-id="78086-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="78086-111">Registrar um aplicativo com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="78086-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="78086-112">Configure a biblioteca do aplicativo toouse Olá ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="78086-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="78086-113">Use hello ADAL4J biblioteca tooissue entrar e solicitações de saída tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="78086-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="78086-114">Imprima dados sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="78086-114">Print out data about hello user.</span></span>

<span data-ttu-id="78086-115">tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="78086-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="78086-116">Você também precisará de um locatário Azure AD no qual tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78086-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="78086-117">Se você não tiver uma, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="78086-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="78086-118">1.  Registrar um aplicativo com o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78086-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="78086-119">tooenable usuários de tooauthenticate seu aplicativo, você precisará primeiro tooregister um novo aplicativo no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="78086-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="78086-120">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78086-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78086-121">Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78086-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="78086-122">Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="78086-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="78086-123">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="78086-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="78086-124">Siga os prompts de saudação e criar um novo **aplicativo Web e/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="78086-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="78086-125">Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos</span><span class="sxs-lookup"><span data-stu-id="78086-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="78086-126">Olá **URL de logon** é Olá a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78086-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="78086-127">padrão do esqueleto Olá é `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="78086-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="78086-128">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="78086-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="78086-129">Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="78086-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="78086-130">De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização.</span><span class="sxs-lookup"><span data-stu-id="78086-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="78086-131">Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78086-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="78086-132">convenção de saudação é toouse `https://<tenant-domain>/<app-name>`, por exemplo, `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="78086-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="78086-133">Uma vez no portal de saudação para seu aplicativo, crie um **chave** de saudação **configurações** página para seu aplicativo e copie-o para baixo.</span><span class="sxs-lookup"><span data-stu-id="78086-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="78086-134">Você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="78086-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="78086-135">2. Configurar a biblioteca do app toouse ADAL4J e os pré-requisitos usando Maven</span><span class="sxs-lookup"><span data-stu-id="78086-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="78086-136">Aqui, configuraremos o protocolo de autenticação ADAL4J toouse Olá OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="78086-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="78086-137">ADAL4J ser usado tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário Olá e obter informações sobre o usuário hello, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="78086-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="78086-138">No diretório raiz de saudação do projeto, abrir/criar `pom.xml` e localize Olá `// TODO: provide dependencies for Maven` e substitua pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="78086-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="78086-139">3. Criar arquivo de Java PublicClient Olá</span><span class="sxs-lookup"><span data-stu-id="78086-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="78086-140">Como indicado acima, vamos usar Olá dados de tooget da API do Graph sobre Olá usuário conectado no.</span><span class="sxs-lookup"><span data-stu-id="78086-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="78086-141">Para este toobe fácil para nós, que deve ser criado ambos um toorepresent arquivo um **objeto de diretório** e hello de toorepresent um arquivo individual **usuário** para que hello OO padrão do Java pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="78086-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="78086-142">Crie um arquivo chamado `DirectoryObject.java` que usaremos toostore de dados básicos sobre qualquer DirectoryObject (você pode se sentir livre toouse isso mais tarde para as consultas de gráfico que você pode fazer).</span><span class="sxs-lookup"><span data-stu-id="78086-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="78086-143">Você pode recortar/colar isso abaixo:</span><span class="sxs-lookup"><span data-stu-id="78086-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="78086-144">Compilar e executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="78086-144">Compile and run hello sample</span></span>
<span data-ttu-id="78086-145">Altere-o diretório raiz de tooyour e execute Olá seguindo o exemplo de saudação do comando toobuild colocar apenas usando `maven`.</span><span class="sxs-lookup"><span data-stu-id="78086-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="78086-146">Isso usará Olá `pom.xml` gravou para dependências de arquivo.</span><span class="sxs-lookup"><span data-stu-id="78086-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="78086-147">Agora você deve ter um arquivo `adal4jsample.war` em seu diretório do `/targets`.</span><span class="sxs-lookup"><span data-stu-id="78086-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="78086-148">Você pode implantar que em seu contêiner Tomcat e visite a URL de saudação</span><span class="sxs-lookup"><span data-stu-id="78086-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="78086-149">É muito fácil toodeploy um WAR com servidores Tomcat mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="78086-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="78086-150">Simplesmente navegar muito`http://localhost:8080/manager/` e siga as instruções de saudação carregar o ' adal4jsample.war' arquivo.</span><span class="sxs-lookup"><span data-stu-id="78086-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="78086-151">Ele será deployment automático para você com o ponto de extremidade correto hello.</span><span class="sxs-lookup"><span data-stu-id="78086-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="78086-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78086-152">Next Steps</span></span>
<span data-ttu-id="78086-153">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="78086-153">Congratulations!</span></span> <span data-ttu-id="78086-154">Você agora tem um aplicativo Java que tem Olá capacidade tooauthenticate usuários de trabalho, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="78086-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="78086-155">Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="78086-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="78086-156">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="78086-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

