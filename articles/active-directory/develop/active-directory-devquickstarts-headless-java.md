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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Usando o aplicativo de linha de comando do Java tooAccess uma API com o Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

O AD do Azure torna simple e direto toooutsource gerenciamento de identidade do seu aplicativo web, fornecendo a única entrada e saída com apenas algumas linhas de código.  Em aplicativos da web de Java, você pode fazer isso usando a implementação da Microsoft da saudação ADAL4J dirigida pela comunidade.

  Aqui usaremos o ADAL4J para:

* Entrada hello usuário no aplicativo hello usando o Azure AD como provedor de identidade hello.
* Exiba algumas informações sobre o usuário hello.
* Entrada hello usuário fora do aplicativo hello.

Em ordem toodo isso, você precisará:

1. Registrar um aplicativo com o Active Directory do Azure
2. Configure a biblioteca do aplicativo toouse Olá ADAL4J.
3. Use hello ADAL4J biblioteca tooissue entrar e solicitações de saída tooAzure AD.
4. Imprima dados sobre o usuário hello.

tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Você também precisará de um locatário Azure AD no qual tooregister seu aplicativo.  Se você não tiver uma, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Registrar um aplicativo com o AD do Azure
tooenable usuários de tooauthenticate seu aplicativo, você precisará primeiro tooregister um novo aplicativo no seu locatário.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.
4. Clique em **Registros do Aplicativo** e escolha **Adicionar**.
5. Siga os prompts de saudação e criar um novo **aplicativo Web e/ou WebAPI**.
  * Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos
  * Olá **URL de logon** é Olá a URL base do seu aplicativo.  padrão do esqueleto Olá é `http://localhost:8080/adal4jsample/`.
6. Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.  Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.
7. De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização. Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.  convenção de saudação é toouse `https://<tenant-domain>/<app-name>`, por exemplo, `http://localhost:8080/adal4jsample/`.

Uma vez no portal de saudação para seu aplicativo, crie um **chave** de saudação **configurações** página para seu aplicativo e copie-o para baixo.  Você precisará dele em breve.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Configurar a biblioteca do app toouse ADAL4J e os pré-requisitos usando Maven
Aqui, configuraremos o protocolo de autenticação ADAL4J toouse Olá OpenID Connect.  ADAL4J ser usado tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário Olá e obter informações sobre o usuário hello, entre outras coisas.

* No diretório raiz de saudação do projeto, abrir/criar `pom.xml` e localize Olá `// TODO: provide dependencies for Maven` e substitua pelo seguinte hello:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Criar arquivo de Java PublicClient Olá
Como indicado acima, vamos usar Olá dados de tooget da API do Graph sobre Olá usuário conectado no. Para este toobe fácil para nós, que deve ser criado ambos um toorepresent arquivo um **objeto de diretório** e hello de toorepresent um arquivo individual **usuário** para que hello OO padrão do Java pode ser usado.

* Crie um arquivo chamado `DirectoryObject.java` que usaremos toostore de dados básicos sobre qualquer DirectoryObject (você pode se sentir livre toouse isso mais tarde para as consultas de gráfico que você pode fazer). Você pode recortar/colar isso abaixo:

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


## <a name="compile-and-run-hello-sample"></a>Compilar e executar o exemplo hello
Altere-o diretório raiz de tooyour e execute Olá seguindo o exemplo de saudação do comando toobuild colocar apenas usando `maven`. Isso usará Olá `pom.xml` gravou para dependências de arquivo.

`$ mvn package`

Agora você deve ter um arquivo `adal4jsample.war` em seu diretório do `/targets`. Você pode implantar que em seu contêiner Tomcat e visite a URL de saudação 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> É muito fácil toodeploy um WAR com servidores Tomcat mais recentes de saudação. Simplesmente navegar muito`http://localhost:8080/manager/` e siga as instruções de saudação carregar o ' adal4jsample.war' arquivo. Ele será deployment automático para você com o ponto de extremidade correto hello.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Parabéns! Você agora tem um aplicativo Java que tem Olá capacidade tooauthenticate usuários de trabalho, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário Olá.  Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), ou você pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

