---
title: "aaaHow toouse Olá Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização Spring no registro de contêiner do Azure tooAzure do serviço de aplicativo"
description: "Este tutorial irá orientá-lo embora Olá etapas toodeploy um aplicativo de inicialização de Spring no registro de contêiner do Azure tooAzure tooAzure do serviço de aplicativo usando um plug-in Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="05c65-103">Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização Spring no registro de contêiner do Azure tooAzure do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="05c65-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="05c65-104">Olá  **[Spring Framework]**  é uma estrutura de código-fonte aberto popular que ajuda os desenvolvedores Java criar web, móveis e aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="05c65-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="05c65-105">Este tutorial usa um aplicativo de exemplo criado usando [Spring inicialização], uma abordagem orientada a convenção para usar Spring tooget iniciado rapidamente.</span><span class="sxs-lookup"><span data-stu-id="05c65-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="05c65-106">Este artigo demonstra como toodeploy tooAzure de aplicativo de inicialização Spring um exemplo do registro do contêiner e, em seguida, use hello Maven plug-in para aplicativos Web do Azure toodeploy tooAzure seu aplicativo do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05c65-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="05c65-107">Olá Maven plug-in para aplicativos Web do Azure está disponível como uma visualização.</span><span class="sxs-lookup"><span data-stu-id="05c65-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="05c65-108">Por enquanto, somente a publicação FTP tem suporte, embora recursos adicionais foram planejados para Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="05c65-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="05c65-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05c65-109">Prerequisites</span></span>

<span data-ttu-id="05c65-110">Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="05c65-111">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="05c65-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="05c65-112">Olá [Azure Interface de linha de comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="05c65-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="05c65-113">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="05c65-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="05c65-114">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="05c65-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="05c65-115">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="05c65-115">A [Git] client.</span></span>
* <span data-ttu-id="05c65-116">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="05c65-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="05c65-117">Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="05c65-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="05c65-118">Exemplo de hello clone Spring inicialização no aplicativo web de Docker</span><span class="sxs-lookup"><span data-stu-id="05c65-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="05c65-119">Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="05c65-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="05c65-120">Abra um prompt de comando ou a janela do terminal e criar um diretório local toohold seu aplicativo de inicialização de Spring e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="05c65-121">-- ou --</span><span class="sxs-lookup"><span data-stu-id="05c65-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="05c65-122">Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório Olá criado; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="05c65-123">Alterar diretório toohello concluída projeto; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="05c65-124">Criar arquivo JAR de saudação usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="05c65-125">Quando o aplicativo da web de saudação tiver sido criado, iniciar Olá web app usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="05c65-126">Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="05c65-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="05c65-127">Por exemplo, você pode usar o hello comando a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="05c65-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="05c65-128">Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo**</span><span class="sxs-lookup"><span data-stu-id="05c65-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="05c65-130">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="05c65-130">Create an Azure service principal</span></span>

<span data-ttu-id="05c65-131">Nesta seção, você criará um Azure entidade de serviço que Olá usos de plug-in Maven durante a implantação de seu contêiner tooAzure.</span><span class="sxs-lookup"><span data-stu-id="05c65-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="05c65-132">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="05c65-132">Open a command prompt.</span></span>

1. <span data-ttu-id="05c65-133">Entre em sua conta do Azure usando Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="05c65-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="05c65-134">Siga Olá instruções toocomplete Olá processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="05c65-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="05c65-135">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="05c65-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="05c65-136">Onde `uuuuuuuu` é o nome de usuário hello e `pppppppp` é a senha Olá Olá entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05c65-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="05c65-137">Azure responde com JSON que é semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-137">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="05c65-138">Você usará os valores de saudação dessa resposta JSON quando você configura Olá Maven plug-in toodeploy tooAzure seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="05c65-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="05c65-139">Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de espaço reservado, que são usados em toomake Este exemplo-toomap mais fácil esses elementos de respectivos do tootheir valores quando você configura o Maven `settings.xml` arquivo hello lado seção.</span><span class="sxs-lookup"><span data-stu-id="05c65-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="05c65-140">Criar um registro de contêiner do Azure usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="05c65-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="05c65-141">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="05c65-141">Open a command prompt.</span></span>

1. <span data-ttu-id="05c65-142">Faça logon no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="05c65-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="05c65-143">Crie um grupo de recursos de saudação recursos do Azure, que você usará neste artigo:</span><span class="sxs-lookup"><span data-stu-id="05c65-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="05c65-144">Substitua `wingtiptoysresources` neste exemplo por um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="05c65-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="05c65-145">Crie um registro de contêiner do Azure privada no grupo de recursos de saudação para seu aplicativo de inicialização de Spring:</span><span class="sxs-lookup"><span data-stu-id="05c65-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="05c65-146">Substitua `wingtiptoysregistry` neste exemplo por um nome exclusivo para seu registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="05c65-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="05c65-147">Recupere a senha de saudação para o registro de contêiner:</span><span class="sxs-lookup"><span data-stu-id="05c65-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="05c65-148">O Azure responderá com sua senha; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="05c65-149">Adicione seu registro de contêiner do Azure e configurações do serviço do Azure tooyour principal Maven</span><span class="sxs-lookup"><span data-stu-id="05c65-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="05c65-150">Abra o Maven `settings.xml` arquivo em um editor de texto; este arquivo pode estar em um caminho como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="05c65-151">Adicionar as configurações de acesso de registro de contêiner do Azure da seção anterior Olá este artigo toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="05c65-152">Em que:</span><span class="sxs-lookup"><span data-stu-id="05c65-152">Where:</span></span>
   <span data-ttu-id="05c65-153">Elemento</span><span class="sxs-lookup"><span data-stu-id="05c65-153">Element</span></span> | <span data-ttu-id="05c65-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="05c65-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="05c65-155">Contém o nome de saudação do registro do contêiner do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="05c65-156">Contém o nome de saudação do registro do contêiner do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="05c65-157">Contém a senha de saudação recuperada na seção anterior Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="05c65-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="05c65-158">Adicionar as configurações de serviço do Azure principal de uma seção anterior de toohello este artigo `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="05c65-159">Em que:</span><span class="sxs-lookup"><span data-stu-id="05c65-159">Where:</span></span>
   <span data-ttu-id="05c65-160">Elemento</span><span class="sxs-lookup"><span data-stu-id="05c65-160">Element</span></span> | <span data-ttu-id="05c65-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="05c65-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="05c65-162">Especifica um nome exclusivo que Maven usa toolook suas configurações de segurança quando você implanta seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="05c65-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="05c65-163">Contém Olá `appId` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05c65-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="05c65-164">Contém Olá `tenant` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05c65-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="05c65-165">Contém Olá `password` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05c65-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="05c65-166">Define o ambiente de nuvem do Azure de destino hello, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="05c65-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="05c65-167">(Uma lista completa dos ambientes está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação)</span><span class="sxs-lookup"><span data-stu-id="05c65-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="05c65-168">Salve e feche o hello *settings.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="05c65-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="05c65-169">Criar imagem de contêiner de seu Docker e enviar por push-tooyour registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="05c65-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="05c65-170">Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring (por exemplo "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra hello *pom.xml* arquivo com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="05c65-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="05c65-171">Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com valor de servidor de logon Olá para o registro de contêiner do Azure na seção anterior de saudação deste tutorial; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="05c65-172">Em que:</span><span class="sxs-lookup"><span data-stu-id="05c65-172">Where:</span></span>
   <span data-ttu-id="05c65-173">Elemento</span><span class="sxs-lookup"><span data-stu-id="05c65-173">Element</span></span> | <span data-ttu-id="05c65-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="05c65-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="05c65-175">Especifica o nome de saudação do registro do contêiner do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="05c65-176">Especifica a URL de saudação do registro do contêiner do Azure privada, que é derivado acrescentando ". azurecr.io" toohello nome do registro do contêiner privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="05c65-177">Verifique `<plugin>` Olá plug-in de Docker em seu *pom.xml* arquivo contém propriedades correto Olá Olá servidor endereço e o registro do nome de logon da etapa anterior Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="05c65-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="05c65-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="05c65-179">Em que:</span><span class="sxs-lookup"><span data-stu-id="05c65-179">Where:</span></span>
   <span data-ttu-id="05c65-180">Elemento</span><span class="sxs-lookup"><span data-stu-id="05c65-180">Element</span></span> | <span data-ttu-id="05c65-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="05c65-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="05c65-182">Especifica a propriedade Olá que contém o nome do registro do contêiner do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="05c65-183">Especifica a propriedade Olá que contém a URL de saudação do registro do contêiner do Azure privado.</span><span class="sxs-lookup"><span data-stu-id="05c65-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="05c65-184">Navegue toohello concluída diretório do projeto para o aplicativo de inicialização de Spring e executar Olá após o aplicativo do comando toorebuild hello e enviar por push Olá contêiner tooyour registro de contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="05c65-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="05c65-185">OPCIONAL: Procurar toohello [portal do Azure] e verifique se não há imagem de contêiner do Docker chamada **gs spring-inicialização docker** no registro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="05c65-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Verificar o contêiner no Portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="05c65-187">Personalizar sua pom.xml, em seguida, compilar e implantar seu contêiner tooAzure</span><span class="sxs-lookup"><span data-stu-id="05c65-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="05c65-188">Olá abrir `pom.xml` de arquivo para o seu aplicativo de inicialização de Spring em um editor de texto e localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="05c65-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="05c65-189">Esse elemento deve ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="05c65-190">Há vários valores que você pode modificar para plug-in do hello Maven e uma descrição detalhada de cada um desses elementos está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação.</span><span class="sxs-lookup"><span data-stu-id="05c65-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="05c65-191">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="05c65-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="05c65-192">Elemento</span><span class="sxs-lookup"><span data-stu-id="05c65-192">Element</span></span> | <span data-ttu-id="05c65-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="05c65-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="05c65-194">Especifica a versão de saudação do hello [Maven plug-in para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="05c65-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="05c65-195">Você deve verificar a versão Olá listado no hello [repositório Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) Olá tooensure que você está usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="05c65-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="05c65-196">Especifica as informações de autenticação de saudação do Azure, que neste exemplo contém um `<serverId>` elemento que contém `azure-auth`; Maven usa toolook esse valor valores principal de serviço do Azure Olá em seu Maven *settings.xml* arquivo, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="05c65-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="05c65-197">Especifica o grupo de recursos de destino hello, que é `wingtiptoysresources` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="05c65-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="05c65-198">grupo de recursos de saudação será criado durante a implantação se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="05c65-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="05c65-199">Especifica o nome do destino de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="05c65-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="05c65-200">Neste exemplo, o nome de destino de saudação é `maven-linux-app-${maven.build.timestamp}`, onde hello `${maven.build.timestamp}` sufixo é acrescentado em conflito de tooavoid neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="05c65-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="05c65-201">(Olá timestamp é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo hello.)</span><span class="sxs-lookup"><span data-stu-id="05c65-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="05c65-202">Especifica a região de destino hello, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="05c65-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="05c65-203">(Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="05c65-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="05c65-204">Especifica as propriedades de saudação que contêm o nome de saudação e a URL do seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="05c65-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="05c65-205">Especifica qualquer configurações exclusivas para Maven toouse ao implantar seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="05c65-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="05c65-206">Neste exemplo, um `<property>` elemento contém um par de nome/valor de elementos filho que especifique a porta Olá para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05c65-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="05c65-207">número de porta de Olá Olá configurações toochange neste exemplo somente são necessárias quando você estiver alterando a porta de saudação do padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="05c65-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="05c65-208">No prompt de comando hello ou janela de terminal que você estava usando anteriormente, recriar o arquivo de JAR de hello usando Maven se você tiver feito qualquer toohello alterações *pom.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="05c65-209">Implantar seu tooAzure de aplicativo web usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c65-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="05c65-210">Maven implantará seu tooAzure de aplicativo da web; Se o aplicativo da web de saudação ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="05c65-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="05c65-211">Se região Olá que você especifica no hello `<region>` elemento da sua *pom.xml* arquivo não tem servidores suficientes disponíveis quando você inicia a implantação, você poderá ver um toohello semelhante erro exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="05c65-212">Se isso acontecer, você pode especificar que outra região e execute novamente Olá Maven comando toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05c65-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="05c65-213">Quando sua web tiver sido implantada, você será capaz de toomanage usando Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="05c65-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="05c65-214">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="05c65-214">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="05c65-216">E Olá URL para seu aplicativo web será listado no hello **visão geral** para seu aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="05c65-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinando Olá URL para seu aplicativo web][AP02]

## <a name="next-steps"></a><span data-ttu-id="05c65-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05c65-218">Next steps</span></span>

<span data-ttu-id="05c65-219">Para obter mais informações sobre Olá diversas tecnologias abordadas neste artigo, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c65-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="05c65-220">[Maven plug-in para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="05c65-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="05c65-221">Faça logon no tooAzure de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="05c65-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="05c65-222">Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="05c65-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="05c65-223">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="05c65-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="05c65-224">[Plug-in do Docker para o Maven]</span><span class="sxs-lookup"><span data-stu-id="05c65-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Maven plug-in para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
