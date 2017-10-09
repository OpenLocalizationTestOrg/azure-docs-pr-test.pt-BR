---
title: "aaaHow toouse Olá Spring inicialização inicial com uma API de documentos do Azure Cosmos DB"
description: "Saiba como tooconfigure um aplicativo criado com hello Spring inicialização inicializador com hello API DocumentDB do Azure Cosmos banco de dados."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Como toouse Olá Spring inicial de inicialização com a API do Azure Cosmos banco de dados DocumentDB

## <a name="overview"></a>Visão geral

Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos. os desenvolvedores de toohelp começar com a inicialização de Spring, vários pacotes de inicialização de Spring de exemplo estão disponíveis em <https://github.com/spring-guides/>. Além disso toochoosing de lista de saudação de inicialização Spring básica projetos, hello  **[Spring Initializr]**  ajuda os desenvolvedores a começar a criar aplicativos personalizados de inicialização de Spring.

Banco de dados do Azure Cosmos é um serviço de banco de dados distribuída globalmente que permite aos desenvolvedores toowork com dados usando uma variedade de APIs padrão, como documentos, MongoDB, gráfico e APIs de tabela. Início de inicialização de Spring da Microsoft permite que os aplicativos de inicialização Spring de toouse os desenvolvedores que se integram facilmente com o banco de dados do Azure Cosmos por meio de APIs do DocumentDB.

Este artigo demonstra como criar um Azure Cosmos DB usando Olá portal do Azure, usando Olá **Initializr Spring** toocreate um aplicativo java personalizados e, em seguida, adicionar Olá Spring inicialização Starter funcionalidade tooyour personalizado aplicativo toostore dados e recuperar dados do seu banco de dados do Azure Cosmos usando Olá API DocumentDB.

## <a name="prerequisites"></a>Pré-requisitos

Olá pré-requisitos a seguir é necessários na ordem toofollow Olá etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].

* Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.

* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Criar um banco de dados do Azure Cosmos usando Olá portal do Azure

1. Procurar toohello Azure portal em <https://portal.azure.com/> e clique em **+ novo**.

   ![Portal do Azure][AZ01]

1. Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.

   ![Portal do Azure][AZ02]

1. Em Olá **o banco de dados do Azure Cosmos** insira Olá informações a seguir:

   * Insira um único **ID**, que você usará como hello URI para o banco de dados. Por exemplo: *wingtiptoysdata.documents.azure.com*.
   * Escolha **SQL (banco de dados de documento)** para Olá API.
   * Escolha Olá **assinatura** você deseja toouse para seu banco de dados.
   * Especifique se toocreate um novo **grupo de recursos** para seu banco de dados, ou escolha um grupo de recursos existente.
   * Especifique a saudação **local** para seu banco de dados.
   
   Quando você especificar essas opções, clique em **criar** toocreate seu banco de dados.

   ![Portal do Azure][AZ03]

1. Quando o banco de dados tiver sido criado, ele está listado no seu Azure **painel**, bem como em Olá **todos os recursos** e **o banco de dados do Azure Cosmos** páginas. Você pode clicar em seu banco de dados em qualquer um desses locais tooopen Olá da página de propriedades para seu cache.

   ![Portal do Azure][AZ04]

1. Quando a página de propriedades de saudação do banco de dados é exibida, clique em **chaves de acesso** e copie as URI e chaves de acesso para seu banco de dados; você usará esses valores em seu aplicativo de inicialização de Spring.

   ![Portal do Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Criar um aplicativo de inicialização de Spring simples com hello Initializr Spring

1. Procurar muito<https://start.spring.io/>.

1. Especifique que você deseja toogenerate um **Maven** projeto com **Java**, digite Olá **grupo** e **artefato** nomes para seu aplicativo, e em seguida, clique botão Olá muito**projeto gerar**.

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > Olá Spring Initializr usa Olá **grupo** e **artefato** nome do pacote de saudação nomes toocreate; por exemplo: *com.example.wintiptoys*.
   >

1. Quando solicitado, baixe o caminho de tooa Olá projeto em seu computador local.

   ![Baixe o projeto personalizado do Spring Boot][SI02]

1. Depois de extrair arquivos Olá no sistema local, seu aplicativo de inicialização de Spring simple estará pronto para edição.

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Configurar a saudação de toouse inicialização Spring aplicativo Azure Spring inicialização inicial

1. Localizar Olá *pom.xml* arquivo no diretório de saudação do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -ou-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Localize o arquivo de pom.xml Olá][PM01]

1. Olá abrir *pom.xml* do arquivo em um editor de texto e adicione Olá após toolist linhas de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Editando o arquivo de pom.xml Olá][PM02]

1. Salve e feche o hello *pom.xml* arquivo.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Configurar seu toouse do aplicativo de inicialização Spring seu banco de dados do Azure Cosmos

1. Localizar Olá *application.properties* arquivo hello *recursos* diretório do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -ou-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Localize o arquivo de application.properties Olá][RE01]

1. Olá abrir *application.properties* do arquivo em um editor de texto, adicione Olá arquivo toohello de linhas a seguir e substitua os valores de exemplo hello com propriedades de saudação apropriado para seu banco de dados:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Editando o arquivo de application.properties Olá][RE02]

1. Salve e feche o hello *application.properties* arquivo.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Adicionar a funcionalidade de banco de dados básicos de tooimplement de código de exemplo

Nesta seção você criará duas classes Java para armazenar dados de usuário e, em seguida, você pode modificar sua classe de aplicativo principal toocreate uma instância da classe de usuário hello e salvá-lo tooyour banco de dados.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definir uma classe básica para armazenar dados do usuário

1. Criar um novo arquivo denominado *User.java* em Olá mesmo diretório que o arquivo de Java do aplicativo principal.

1. Olá abrir *User.java* do arquivo em um editor de texto e adicione a seguinte Olá linhas toohello arquivo toodefine uma classe de usuário genérica que armazena e recupera os valores no banco de dados:

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. Salve e feche o hello *User.java* arquivo.

### <a name="define-a-data-repository-interface"></a>Defina uma interface de repositório de dados

1. Criar um novo arquivo denominado *UserRepository.java* em Olá mesmo diretório que o arquivo de Java do aplicativo principal.

1. Olá abrir *UserRepository.java* do arquivo em um editor de texto e adicione a seguinte Olá linhas toohello arquivo toodefine uma interface de repositório do usuário que se estende a interface de repositório de documentos saudação padrão:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Salve e feche o hello *UserRepository.java* arquivo.

### <a name="modify-hello-main-application-class"></a>Modificar a classe de aplicativo principal Olá

1. Localizar arquivo de Java Olá principal do aplicativo no diretório do pacote de saudação do seu aplicativo; Por exemplo:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -ou-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Localizar arquivo de Java do aplicativo hello][JV01]

1. Abrir arquivo de Java Olá principal do aplicativo em um editor de texto e adicione Olá arquivo toohello de linhas a seguir:

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. Salve e feche o arquivo de Java Olá principal do aplicativo.

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Abra um prompt de comando e altere a pasta de toohello do diretório onde o *pom.xml* arquivo está localizado, por exemplo:

   `cd C:\SpringBoot\wingtiptoys`

   -ou-

   `cd /users/example/home/wingtiptoys`

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. O aplicativo exibirá várias mensagens de tempo de execução, e você verá uma mensagem de saudação `User: testFirstName testLastName` exibidas tooindicate valores foram armazenados e recuperados do banco de dados com êxito.

   ![Saída bem-sucedida de um aplicativo hello][JV02]

1. OPCIONAL: Você pode usar Olá tooview portal do Azure Olá conteúdo de seu banco de dados do Azure Cosmos Olá na página de propriedades do banco de dados clicando em **Document Explorer**e, em seguida, selecionar e item de saudação do hello exibido lista tooview conteúdo.

   ![Usando Olá Document Explorer tooview seus dados][JV03]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o banco de dados do Azure Cosmos e Java, consulte Olá artigos a seguir:

* [Documentação do Azure Cosmos DB].

* [Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Java e Olá portal do Azure][Build a DocumentDB API app with Java]

Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:

* [Iniciador do DocumenDB do Spring Boot para Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Executando um aplicativo de inicialização de Spring em um Cluster de Kubernetes hello Azure serviço de contêiner](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

<!-- URL List -->

[Documentação do Azure Cosmos DB]: /azure/cosmos-db/
[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
