---
title: Exportar os certificados do Emulador do Azure Cosmos DB | Microsoft Docs
description: "Ao desenvolver em linguagens e em tempos de execução que não usam o Repositório de Certificados do Windows, você precisará exportar e gerenciar os certificados SSL. Esta postagem fornece instruções passo a passo."
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
ms.openlocfilehash: 4add5028d50972316902cecd8c399781c012cb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="52d38-105">Exportar os certificados do Emulador do Azure Cosmos DB para uso com Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="52d38-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="52d38-106">**Baixar o Emulador**</span><span class="sxs-lookup"><span data-stu-id="52d38-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="52d38-107">O Emulador do Azure Cosmos DB fornece um ambiente local que emula o serviço Azure Cosmos DB para fins de desenvolvimento, incluindo seu uso de conexões SSL.</span><span class="sxs-lookup"><span data-stu-id="52d38-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="52d38-108">Esta postagem demonstra como exportar os certificados SSL para uso em linguagens e em tempos de execução que não são integrados ao Repositório de Certificados do Windows, por exemplo, Java, que usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) e Python, que usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html) e .Node.js que usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="52d38-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="52d38-109">Leia mais sobre o emulador em [Usar o Emulador do Azure Cosmos DB para desenvolvimento e teste](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="52d38-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="52d38-110">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="52d38-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52d38-111">Rotação de certificados</span><span class="sxs-lookup"><span data-stu-id="52d38-111">Rotating certificates</span></span>
> * <span data-ttu-id="52d38-112">Exportando o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="52d38-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="52d38-113">Aprendendo a usar o certificado no Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="52d38-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="52d38-114">Rotação de certificação</span><span class="sxs-lookup"><span data-stu-id="52d38-114">Certification rotation</span></span>

<span data-ttu-id="52d38-115">Os certificados no Emulador Local do Azure Cosmos DB são gerados na primeira vez que o emulador é executado.</span><span class="sxs-lookup"><span data-stu-id="52d38-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="52d38-116">Há dois certificados.</span><span class="sxs-lookup"><span data-stu-id="52d38-116">There are two certificates.</span></span> <span data-ttu-id="52d38-117">Um usado para conexão com o emulador do local, e outro para gerenciar segredos no emulador.</span><span class="sxs-lookup"><span data-stu-id="52d38-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="52d38-118">O certificado que você quer exportar é o certificado de conexão com o nome amigável "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="52d38-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="52d38-119">Os dois certificados podem ser gerados novamente clicando em **Redefinir Dados**, conforme mostrado abaixo no Emulador do Azure Cosmos DB em execução na Bandeja do Windows.</span><span class="sxs-lookup"><span data-stu-id="52d38-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="52d38-120">Se você gerar novamente os certificados e instalá-los no repositório de certificados Java, ou usá-los em outro lugar, será necessário atualizá-los, caso contrário, seu aplicativo não conectará mais ao emulador local.</span><span class="sxs-lookup"><span data-stu-id="52d38-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Redefinição de dados do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="52d38-122">Como exportar o certificado SSL do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="52d38-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="52d38-123">Inicie o gerenciador de Certificados do Windows executando certlm.msc, navegue até a pasta Pessoal-> Certificados e abra o certificado com o nome amigável **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="52d38-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Etapa 1 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="52d38-125">Clique em **Detalhes** e depois em **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d38-125">Click on **Details** then **OK**.</span></span>

    ![Etapa 2 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="52d38-127">Clique em **Copiar para arquivo...**.</span><span class="sxs-lookup"><span data-stu-id="52d38-127">Click **Copy to File...**.</span></span>

    ![Etapa 3 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="52d38-129">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="52d38-129">Click **Next**.</span></span>

    ![Etapa 4 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="52d38-131">Clique em **Não, não exportar a chave privada** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="52d38-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Etapa 5 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="52d38-133">Clique em **X.509 codificado em Base-64 (.CER)** e depois em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="52d38-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Etapa 6 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="52d38-135">Dê um nome ao certificado.</span><span class="sxs-lookup"><span data-stu-id="52d38-135">Give the certificate a name.</span></span> <span data-ttu-id="52d38-136">Nesse caso, **documentdbemulatorcert** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="52d38-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Etapa 7 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="52d38-138">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="52d38-138">Click **Finish**.</span></span>

    ![Etapa 8 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="52d38-140">Como usar o certificado em Java</span><span class="sxs-lookup"><span data-stu-id="52d38-140">How to use the certificate in Java</span></span>

<span data-ttu-id="52d38-141">Durante a execução de aplicativos Java ou MongoDB que usam o cliente Java, é mais fácil instalar o certificado no repositório de certificados Java padrão do que passar os sinalizadores "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>.</span><span class="sxs-lookup"><span data-stu-id="52d38-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="52d38-142">Por exemplo, o [aplicativo de demonstração Java](https://localhost:8081/_explorer/index.html) incluído depende do repositório de certificados padrão.</span><span class="sxs-lookup"><span data-stu-id="52d38-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="52d38-143">Siga as instruções em [Adicionar um certificado ao Repositório de Certificados de AC Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) para importar o certificado X.509 no repositório de certificados Java padrão.</span><span class="sxs-lookup"><span data-stu-id="52d38-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="52d38-144">Lembre-se de que você trabalhará no diretório %JAVA_HOME% durante a execução da keytool.</span><span class="sxs-lookup"><span data-stu-id="52d38-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="52d38-145">Após a instalação do certificado SSL “CosmosDBEmulatorCertificate”, seu aplicativo deverá conseguir se conectar e usar o Emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52d38-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="52d38-146">Se você continuar tendo problemas, siga o artigo [Depuração de conexões SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html).</span><span class="sxs-lookup"><span data-stu-id="52d38-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="52d38-147">É muito provável que o certificado não esteja instalado no repositório %JAVA_HOME%/jre/lib/security/cacerts.</span><span class="sxs-lookup"><span data-stu-id="52d38-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="52d38-148">Por exemplo, se você tiver várias versões do Java instaladas, seu aplicativo poderá usar um repositório de cacerts diferente daquele que você atualizou.</span><span class="sxs-lookup"><span data-stu-id="52d38-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="52d38-149">Como usar o certificado em Python</span><span class="sxs-lookup"><span data-stu-id="52d38-149">How to use the certificate in Python</span></span>

<span data-ttu-id="52d38-150">Por padrão, o [SDK do Python (versão 2.0.0 ou superior)](documentdb-sdk-python.md) para a API do DocumentDB não tentará usar o certificado SSL ao se conectar ao emulador local.</span><span class="sxs-lookup"><span data-stu-id="52d38-150">By default the [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="52d38-151">Se, no entanto, você quiser usar a validação de SSL, siga os exemplos na documentação [Wrappers de soquete Python](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="52d38-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="52d38-152">Como usar o certificado no Node.js</span><span class="sxs-lookup"><span data-stu-id="52d38-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="52d38-153">Por padrão, o [SDK do Node.js (versão 1.10.1 ou superior)](documentdb-sdk-node.md) para a API do DocumentDB não tentará usar o certificado SSL ao se conectar ao emulador local.</span><span class="sxs-lookup"><span data-stu-id="52d38-153">By default the [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="52d38-154">Se, no entanto, você quiser usar a validação de SSL, siga os exemplos na [Documentação do Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="52d38-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52d38-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52d38-155">Next steps</span></span>

<span data-ttu-id="52d38-156">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52d38-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52d38-157">Trocou certificados</span><span class="sxs-lookup"><span data-stu-id="52d38-157">Rotated certificates</span></span>
> * <span data-ttu-id="52d38-158">Exportou o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="52d38-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="52d38-159">Aprendeu a usar o certificado no Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="52d38-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="52d38-160">Agora você pode seguir para a seção Conceitos para obter mais informações sobre o Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52d38-160">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52d38-161">Distribuição global</span><span class="sxs-lookup"><span data-stu-id="52d38-161">Global distribution</span></span>](distribute-data-globally.md) 
