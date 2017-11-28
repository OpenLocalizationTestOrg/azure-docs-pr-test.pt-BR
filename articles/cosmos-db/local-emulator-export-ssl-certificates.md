---
title: "certificados de emulador do Azure Cosmos DB Olá aaaExport | Microsoft Docs"
description: "Ao desenvolver em idiomas e tempos de execução que não usam o repositório de certificados do Windows hello será necessário tooexport e gerencie certificados SSL de saudação. Esta postagem fornece instruções passo a passo."
services: cosmos-db
documentationcenter: 
keywords: Emulador do Azure Cosmos DB
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="4865b-105">Exportar hello Azure Cosmos DB emulador certificados para uso com o Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="4865b-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="4865b-106">**Baixar Olá emulador**</span><span class="sxs-lookup"><span data-stu-id="4865b-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="4865b-107">Hello Azure Cosmos DB emulador fornece um ambiente local que emula Olá serviço de banco de dados do Azure Cosmos para fins de desenvolvimento, incluindo o uso de conexões SSL.</span><span class="sxs-lookup"><span data-stu-id="4865b-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="4865b-108">Esta postagem demonstra como tooexport Olá SSL certificados para uso em idiomas e tempos de execução que não integram Olá repositório de certificados do Windows, como Java que usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) e Python que usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html) e Node. js que usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="4865b-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="4865b-109">Você pode ler mais sobre o emulador de saudação do [Olá Use Azure Cosmos DB Emulator para desenvolvimento e teste](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="4865b-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="4865b-110">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4865b-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4865b-111">Rotação de certificados</span><span class="sxs-lookup"><span data-stu-id="4865b-111">Rotating certificates</span></span>
> * <span data-ttu-id="4865b-112">Exportando o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="4865b-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="4865b-113">Aprender como toouse Olá certificado em Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="4865b-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="4865b-114">Rotação de certificação</span><span class="sxs-lookup"><span data-stu-id="4865b-114">Certification rotation</span></span>

<span data-ttu-id="4865b-115">Certificados no hello que emulador Local do banco de dados do Azure Cosmos são gerados Olá primeira execução do emulador hello.</span><span class="sxs-lookup"><span data-stu-id="4865b-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="4865b-116">Há dois certificados.</span><span class="sxs-lookup"><span data-stu-id="4865b-116">There are two certificates.</span></span> <span data-ttu-id="4865b-117">Um usado para conectar um emulador local toohello e para gerenciar segredos no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="4865b-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="4865b-118">Olá certificado tooexport é certificado de conexão de saudação com o nome amigável do hello "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="4865b-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="4865b-119">Ambos os certificados podem ser regenerados clicando **Redefinir dados** conforme mostrado abaixo do Azure Cosmos DB emulador em execução no hello bandeja do Windows.</span><span class="sxs-lookup"><span data-stu-id="4865b-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="4865b-120">Se você gerar novamente os certificados de saudação e instalou-los no repositório de certificados do Java hello ou usá-los em outro lugar, você precisará tooupdate-las, caso contrário, se seu aplicativo não conectará toohello um emulador local.</span><span class="sxs-lookup"><span data-stu-id="4865b-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Redefinição de dados do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="4865b-122">Como tooexport Olá certificado SSL de banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="4865b-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="4865b-123">Inicie o Gerenciador de certificados do Windows hello executando certlm.msc e navegue toohello pessoal -> pasta certificados e certificado Olá aberta com o nome amigável da saudação **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="4865b-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Etapa 1 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="4865b-125">Clique em **Detalhes** e depois em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4865b-125">Click on **Details** then **OK**.</span></span>

    ![Etapa 2 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="4865b-127">Clique em **copiar tooFile... **.</span><span class="sxs-lookup"><span data-stu-id="4865b-127">Click **Copy tooFile...**.</span></span>

    ![Etapa 3 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="4865b-129">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4865b-129">Click **Next**.</span></span>

    ![Etapa 4 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="4865b-131">Clique em **Não, não exportar a chave privada** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4865b-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Etapa 5 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="4865b-133">Clique em **X.509 codificado em Base-64 (.CER)** e depois em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4865b-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Etapa 6 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="4865b-135">Dê um nome de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="4865b-135">Give hello certificate a name.</span></span> <span data-ttu-id="4865b-136">Nesse caso, **documentdbemulatorcert** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4865b-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Etapa 7 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="4865b-138">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4865b-138">Click **Finish**.</span></span>

    ![Etapa 8 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="4865b-140">Como toouse Olá certificado em Java</span><span class="sxs-lookup"><span data-stu-id="4865b-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="4865b-141">Durante a execução de aplicativos Java ou MongoDB que usam o cliente de Java Olá é mais fácil certificado de saudação tooinstall no repositório de certificados do hello Java padrão que passando hello "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="4865b-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="4865b-142">Por exemplo hello incluído [aplicativo Java demonstração](https://localhost:8081/_explorer/index.html) depende do repositório de certificados saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="4865b-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="4865b-143">Siga as instruções de Olá Olá [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Olá x. 509 do certificado no repositório de certificados de Java saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="4865b-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="4865b-144">Lembre-Lembre-se estará trabalhando no diretório Olá % JAVA_HOME % durante a execução keytool.</span><span class="sxs-lookup"><span data-stu-id="4865b-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="4865b-145">Uma vez hello "CosmosDBEmulatorCertificate" SSL certificado está instalado seu aplicativo deve ser capaz de tooconnect e use Olá emulador local de banco de dados de Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4865b-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="4865b-146">Se você continuar toohave problemas convém Olá toofollow [conexões de SSL/TLS depuração](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artigo.</span><span class="sxs-lookup"><span data-stu-id="4865b-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="4865b-147">É muito provável certificado Olá não está instalado no repositório de %JAVA_HOME%/jre/lib/security/cacerts hello.</span><span class="sxs-lookup"><span data-stu-id="4865b-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="4865b-148">Por exemplo, se você tiver várias versões instaladas do Java seu aplicativo pode estar usando um repositório cacerts diferentes de Olá uma atualização.</span><span class="sxs-lookup"><span data-stu-id="4865b-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="4865b-149">Como toouse Olá certificado no Python</span><span class="sxs-lookup"><span data-stu-id="4865b-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="4865b-150">Por saudação padrão [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) para Olá API DocumentDB não tente e usar certificado SSL da saudação ao se conectar a um emulador local toohello.</span><span class="sxs-lookup"><span data-stu-id="4865b-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="4865b-151">Se, no entanto, você deseja toouse SSL validação, você pode seguir exemplos Olá Olá [Python soquete wrappers](https://docs.python.org/2/library/ssl.html) documentação.</span><span class="sxs-lookup"><span data-stu-id="4865b-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="4865b-152">Como toouse Olá certificado no Node. js</span><span class="sxs-lookup"><span data-stu-id="4865b-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="4865b-153">Por saudação padrão [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) para Olá API DocumentDB não tente e usar certificado SSL da saudação ao se conectar a um emulador local toohello.</span><span class="sxs-lookup"><span data-stu-id="4865b-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="4865b-154">Se, no entanto, você deseja toouse SSL validação, você pode seguir exemplos Olá Olá [Node. js documentação](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="4865b-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4865b-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4865b-155">Next steps</span></span>

<span data-ttu-id="4865b-156">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="4865b-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4865b-157">Trocou certificados</span><span class="sxs-lookup"><span data-stu-id="4865b-157">Rotated certificates</span></span>
> * <span data-ttu-id="4865b-158">Certificado SSL hello exportada</span><span class="sxs-lookup"><span data-stu-id="4865b-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="4865b-159">Aprendeu como toouse Olá certificado em Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="4865b-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="4865b-160">Você pode continuar toohello seção conceitos para obter mais informações sobre o banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4865b-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4865b-161">Distribuição global</span><span class="sxs-lookup"><span data-stu-id="4865b-161">Global distribution</span></span>](distribute-data-globally.md) 
