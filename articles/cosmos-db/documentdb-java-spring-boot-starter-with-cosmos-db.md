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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="ac10b-104">Como toouse Olá Spring inicial de inicialização com a API do Azure Cosmos banco de dados DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ac10b-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="ac10b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ac10b-105">Overview</span></span>

<span data-ttu-id="ac10b-106">Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="ac10b-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ac10b-107">Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="ac10b-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ac10b-108">os desenvolvedores de toohelp começar com a inicialização de Spring, vários pacotes de inicialização de Spring de exemplo estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="ac10b-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="ac10b-109">Além disso toochoosing de lista de saudação de inicialização Spring básica projetos, hello  **[Spring Initializr]**  ajuda os desenvolvedores a começar a criar aplicativos personalizados de inicialização de Spring.</span><span class="sxs-lookup"><span data-stu-id="ac10b-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="ac10b-110">Banco de dados do Azure Cosmos é um serviço de banco de dados distribuída globalmente que permite aos desenvolvedores toowork com dados usando uma variedade de APIs padrão, como documentos, MongoDB, gráfico e APIs de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac10b-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="ac10b-111">Início de inicialização de Spring da Microsoft permite que os aplicativos de inicialização Spring de toouse os desenvolvedores que se integram facilmente com o banco de dados do Azure Cosmos por meio de APIs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ac10b-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="ac10b-112">Este artigo demonstra como criar um Azure Cosmos DB usando Olá portal do Azure, usando Olá **Initializr Spring** toocreate um aplicativo java personalizados e, em seguida, adicionar Olá Spring inicialização Starter funcionalidade tooyour personalizado aplicativo toostore dados e recuperar dados do seu banco de dados do Azure Cosmos usando Olá API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ac10b-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac10b-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac10b-113">Prerequisites</span></span>

<span data-ttu-id="ac10b-114">Olá pré-requisitos a seguir é necessários na ordem toofollow Olá etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="ac10b-115">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="ac10b-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="ac10b-116">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ac10b-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="ac10b-117">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ac10b-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="ac10b-118">Criar um banco de dados do Azure Cosmos usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ac10b-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="ac10b-119">Procurar toohello Azure portal em <https://portal.azure.com/> e clique em **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="ac10b-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portal do Azure][AZ01]

1. <span data-ttu-id="ac10b-121">Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ac10b-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portal do Azure][AZ02]

1. <span data-ttu-id="ac10b-123">Em Olá **o banco de dados do Azure Cosmos** insira Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac10b-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="ac10b-124">Insira um único **ID**, que você usará como hello URI para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ac10b-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="ac10b-125">Por exemplo: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ac10b-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="ac10b-126">Escolha **SQL (banco de dados de documento)** para Olá API.</span><span class="sxs-lookup"><span data-stu-id="ac10b-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="ac10b-127">Escolha Olá **assinatura** você deseja toouse para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ac10b-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="ac10b-128">Especifique se toocreate um novo **grupo de recursos** para seu banco de dados, ou escolha um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="ac10b-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="ac10b-129">Especifique a saudação **local** para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ac10b-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="ac10b-130">Quando você especificar essas opções, clique em **criar** toocreate seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ac10b-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Portal do Azure][AZ03]

1. <span data-ttu-id="ac10b-132">Quando o banco de dados tiver sido criado, ele está listado no seu Azure **painel**, bem como em Olá **todos os recursos** e **o banco de dados do Azure Cosmos** páginas.</span><span class="sxs-lookup"><span data-stu-id="ac10b-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="ac10b-133">Você pode clicar em seu banco de dados em qualquer um desses locais tooopen Olá da página de propriedades para seu cache.</span><span class="sxs-lookup"><span data-stu-id="ac10b-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portal do Azure][AZ04]

1. <span data-ttu-id="ac10b-135">Quando a página de propriedades de saudação do banco de dados é exibida, clique em **chaves de acesso** e copie as URI e chaves de acesso para seu banco de dados; você usará esses valores em seu aplicativo de inicialização de Spring.</span><span class="sxs-lookup"><span data-stu-id="ac10b-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portal do Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="ac10b-137">Criar um aplicativo de inicialização de Spring simples com hello Initializr Spring</span><span class="sxs-lookup"><span data-stu-id="ac10b-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="ac10b-138">Procurar muito<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ac10b-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ac10b-139">Especifique que você deseja toogenerate um **Maven** projeto com **Java**, digite Olá **grupo** e **artefato** nomes para seu aplicativo, e em seguida, clique botão Olá muito**projeto gerar**.</span><span class="sxs-lookup"><span data-stu-id="ac10b-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ac10b-141">Olá Spring Initializr usa Olá **grupo** e **artefato** nome do pacote de saudação nomes toocreate; por exemplo: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="ac10b-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="ac10b-142">Quando solicitado, baixe o caminho de tooa Olá projeto em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="ac10b-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot][SI02]

1. <span data-ttu-id="ac10b-144">Depois de extrair arquivos Olá no sistema local, seu aplicativo de inicialização de Spring simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="ac10b-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="ac10b-146">Configurar a saudação de toouse inicialização Spring aplicativo Azure Spring inicialização inicial</span><span class="sxs-lookup"><span data-stu-id="ac10b-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="ac10b-147">Localizar Olá *pom.xml* arquivo no diretório de saudação do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="ac10b-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="ac10b-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Localize o arquivo de pom.xml Olá][PM01]

1. <span data-ttu-id="ac10b-150">Olá abrir *pom.xml* do arquivo em um editor de texto e adicione Olá após toolist linhas de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="ac10b-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Editando o arquivo de pom.xml Olá][PM02]

1. <span data-ttu-id="ac10b-152">Salve e feche o hello *pom.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="ac10b-153">Configurar seu toouse do aplicativo de inicialização Spring seu banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="ac10b-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="ac10b-154">Localizar Olá *application.properties* arquivo hello *recursos* diretório do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="ac10b-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="ac10b-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Localize o arquivo de application.properties Olá][RE01]

1. <span data-ttu-id="ac10b-157">Olá abrir *application.properties* do arquivo em um editor de texto, adicione Olá arquivo toohello de linhas a seguir e substitua os valores de exemplo hello com propriedades de saudação apropriado para seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ac10b-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Editando o arquivo de application.properties Olá][RE02]

1. <span data-ttu-id="ac10b-159">Salve e feche o hello *application.properties* arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="ac10b-160">Adicionar a funcionalidade de banco de dados básicos de tooimplement de código de exemplo</span><span class="sxs-lookup"><span data-stu-id="ac10b-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="ac10b-161">Nesta seção você criará duas classes Java para armazenar dados de usuário e, em seguida, você pode modificar sua classe de aplicativo principal toocreate uma instância da classe de usuário hello e salvá-lo tooyour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ac10b-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="ac10b-162">Definir uma classe básica para armazenar dados do usuário</span><span class="sxs-lookup"><span data-stu-id="ac10b-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="ac10b-163">Criar um novo arquivo denominado *User.java* em Olá mesmo diretório que o arquivo de Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="ac10b-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ac10b-164">Olá abrir *User.java* do arquivo em um editor de texto e adicione a seguinte Olá linhas toohello arquivo toodefine uma classe de usuário genérica que armazena e recupera os valores no banco de dados:</span><span class="sxs-lookup"><span data-stu-id="ac10b-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="ac10b-165">Salve e feche o hello *User.java* arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="ac10b-166">Defina uma interface de repositório de dados</span><span class="sxs-lookup"><span data-stu-id="ac10b-166">Define a data repository interface</span></span>

1. <span data-ttu-id="ac10b-167">Criar um novo arquivo denominado *UserRepository.java* em Olá mesmo diretório que o arquivo de Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="ac10b-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ac10b-168">Olá abrir *UserRepository.java* do arquivo em um editor de texto e adicione a seguinte Olá linhas toohello arquivo toodefine uma interface de repositório do usuário que se estende a interface de repositório de documentos saudação padrão:</span><span class="sxs-lookup"><span data-stu-id="ac10b-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="ac10b-169">Salve e feche o hello *UserRepository.java* arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="ac10b-170">Modificar a classe de aplicativo principal Olá</span><span class="sxs-lookup"><span data-stu-id="ac10b-170">Modify hello main application class</span></span>

1. <span data-ttu-id="ac10b-171">Localizar arquivo de Java Olá principal do aplicativo no diretório do pacote de saudação do seu aplicativo; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="ac10b-172">-ou-</span><span class="sxs-lookup"><span data-stu-id="ac10b-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Localizar arquivo de Java do aplicativo hello][JV01]

1. <span data-ttu-id="ac10b-174">Abrir arquivo de Java Olá principal do aplicativo em um editor de texto e adicione Olá arquivo toohello de linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac10b-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

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

1. <span data-ttu-id="ac10b-175">Salve e feche o arquivo de Java Olá principal do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="ac10b-176">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ac10b-176">Build and test your app</span></span>

1. <span data-ttu-id="ac10b-177">Abra um prompt de comando e altere a pasta de toohello do diretório onde o *pom.xml* arquivo está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="ac10b-178">-ou-</span><span class="sxs-lookup"><span data-stu-id="ac10b-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="ac10b-179">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac10b-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="ac10b-180">O aplicativo exibirá várias mensagens de tempo de execução, e você verá uma mensagem de saudação `User: testFirstName testLastName` exibidas tooindicate valores foram armazenados e recuperados do banco de dados com êxito.</span><span class="sxs-lookup"><span data-stu-id="ac10b-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Saída bem-sucedida de um aplicativo hello][JV02]

1. <span data-ttu-id="ac10b-182">OPCIONAL: Você pode usar Olá tooview portal do Azure Olá conteúdo de seu banco de dados do Azure Cosmos Olá na página de propriedades do banco de dados clicando em **Document Explorer**e, em seguida, selecionar e item de saudação do hello exibido lista tooview conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ac10b-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Usando Olá Document Explorer tooview seus dados][JV03]

## <a name="next-steps"></a><span data-ttu-id="ac10b-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac10b-184">Next steps</span></span>

<span data-ttu-id="ac10b-185">Para obter mais informações sobre como usar o banco de dados do Azure Cosmos e Java, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac10b-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="ac10b-186">[Documentação do Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="ac10b-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="ac10b-187">[Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Java e Olá portal do Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="ac10b-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="ac10b-188">Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac10b-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="ac10b-189">Iniciador do DocumenDB do Spring Boot para Azure</span><span class="sxs-lookup"><span data-stu-id="ac10b-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="ac10b-190">Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ac10b-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="ac10b-191">Executando um aplicativo de inicialização de Spring em um Cluster de Kubernetes hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="ac10b-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="ac10b-192">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ac10b-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
