---
title: "Criar um aplicativo Web no Serviço de Aplicativo do Azure usando o SDK do Azure para Java"
description: "Aprenda a criar um aplicativo Web no Serviço de Aplicativo do Azure programaticamente, usando o SDK do Azure para Java."
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="03fff-103">Criar um aplicativo Web no Serviço de Aplicativo do Azure usando o SDK do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="03fff-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="03fff-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="03fff-104">Overview</span></span>
<span data-ttu-id="03fff-105">Este passo a passo mostra como criar um SDK do Azure para um aplicativo Java que cria um Aplicativo Web no [Serviço de Aplicativo do Azure][Azure App Service] e depois como implantar um aplicativo nele.</span><span class="sxs-lookup"><span data-stu-id="03fff-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="03fff-106">Ele consiste em duas partes:</span><span class="sxs-lookup"><span data-stu-id="03fff-106">It consists of two parts:</span></span>

* <span data-ttu-id="03fff-107">A parte 1 demonstra como compilar um aplicativo Java que cria um aplicativo da Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="03fff-108">A parte 2 demonstra como criar um aplicativo JSP simples "Olá mundo" e então usar um cliente FTP para implantar o código no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fff-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03fff-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03fff-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="03fff-110">Instalações de software</span><span class="sxs-lookup"><span data-stu-id="03fff-110">Software Installations</span></span>
<span data-ttu-id="03fff-111">O código do aplicativo AzureWebDemo neste artigo foi escrito usando o SDK para Java 0.7.0 do Azure, que pode ser instalado usando o WebPI ([Web Platform Installer][Web Platform Installer]).</span><span class="sxs-lookup"><span data-stu-id="03fff-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="03fff-112">Além disso, certifique-se de usar a versão mais recente do [Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="03fff-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="03fff-113">Depois de instalar o SDK, atualize as dependências em o projeto do Eclipse executando **Atualizar Índice** em **Repositórios Maven**, então adicione novamente a versão mais recente de cada pacote na janela **Dependências**.</span><span class="sxs-lookup"><span data-stu-id="03fff-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="03fff-114">Você pode verificar a versão do software instalado no Eclipse clicando em **Ajuda > Detalhes da instalação**. Você deve ter pelo menos as seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="03fff-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="03fff-115">Pacote para Bibliotecas do Microsoft Azure para Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="03fff-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="03fff-116">Eclipse IDE para desenvolvedores de Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="03fff-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="03fff-117">Criar e configurar recursos de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="03fff-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="03fff-118">Antes de iniciar este procedimento, você precisa ter uma assinatura ativa do Azure e configurar um AD (Active Directory) padrão no Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="03fff-119">Criar um AD (Active Directory) no Azure</span><span class="sxs-lookup"><span data-stu-id="03fff-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="03fff-120">Se você ainda não tem um AD (Active Directory) na sua assinatura do Azure, faça logon no [portal clássico do Azure][Azure classic portal] com sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03fff-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="03fff-121">Se você tiver várias assinaturas, clique em **Assinaturas** e selecione o diretório padrão para a assinatura que deseja usar para este projeto.</span><span class="sxs-lookup"><span data-stu-id="03fff-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="03fff-122">Em seguida, clique em **Aplicar** para alternar para esse modo de exibição de assinatura.</span><span class="sxs-lookup"><span data-stu-id="03fff-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="03fff-123">Selecione **Active Directory** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="03fff-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="03fff-124">**Clique em Novo > Diretório > Criação Personalizada**.</span><span class="sxs-lookup"><span data-stu-id="03fff-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="03fff-125">Em **Adicionar Diretório**, selecione **Criar Novo Diretório**.</span><span class="sxs-lookup"><span data-stu-id="03fff-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="03fff-126">Em **Nome**, insira um nome de diretório.</span><span class="sxs-lookup"><span data-stu-id="03fff-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="03fff-127">Em **Domínio**, insira um nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="03fff-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="03fff-128">Este é um nome de domínio básico que é incluído por padrão com seu diretório; ele tem a forma `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="03fff-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="03fff-129">Você pode nomeá-com base no nome do diretório ou outro nome de domínio que você possua.</span><span class="sxs-lookup"><span data-stu-id="03fff-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="03fff-130">Posteriormente, você pode adicionar outro nome de domínio que sua organização já utilize.</span><span class="sxs-lookup"><span data-stu-id="03fff-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="03fff-131">Em **País ou região**, selecione sua localidade.</span><span class="sxs-lookup"><span data-stu-id="03fff-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="03fff-132">Para saber mais sobre o AD, confira [O que é um diretório do Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="03fff-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="03fff-133">Criar um Certificado de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="03fff-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="03fff-134">O SDK do Azure para Java usa certificados de gerenciamento para autenticar com as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="03fff-135">Estes são certificados X.509 v3 que você usa para autenticar um aplicativo cliente que usa a API de gerenciamento de serviços para atuar em nome do proprietário da assinatura para gerenciar os recursos de assinatura.</span><span class="sxs-lookup"><span data-stu-id="03fff-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="03fff-136">O código neste procedimento usa um certificado autoassinado para autenticar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="03fff-137">Para este procedimento, você precisa criar um certificado e carregá-lo no [portal clássico do Azure][Azure classic portal] com antecedência.</span><span class="sxs-lookup"><span data-stu-id="03fff-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="03fff-138">Isso envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="03fff-138">This involves the following steps:</span></span>

* <span data-ttu-id="03fff-139">Gere um arquivo PFX que represente seu certificado de cliente e salve-o localmente.</span><span class="sxs-lookup"><span data-stu-id="03fff-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="03fff-140">Gere um certificado de gerenciamento (arquivo CER) por meio do arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="03fff-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="03fff-141">Carregue o arquivo CER em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="03fff-142">Converta o arquivo PFX em JKS, já que o Java usa esse formato para autenticar usando certificados.</span><span class="sxs-lookup"><span data-stu-id="03fff-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="03fff-143">Escreva um código de autenticação para o aplicativo, que se refira ao arquivo JKS local.</span><span class="sxs-lookup"><span data-stu-id="03fff-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="03fff-144">Quando você concluir este procedimento, o certificado CER residirá na sua assinatura do Azure e o certificado JKS residirá no disco local.</span><span class="sxs-lookup"><span data-stu-id="03fff-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="03fff-145">Para saber mais sobre gerenciamento de certificados, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="03fff-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="03fff-146">Criar um certificado</span><span class="sxs-lookup"><span data-stu-id="03fff-146">Create a certificate</span></span>
<span data-ttu-id="03fff-147">Para criar seu próprio certificado autoassinado, abra um console de comando em seu sistema operacional e execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="03fff-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="03fff-148">**Observação:** o computador em que você executar esse comando deverá ter o JDK instalado.</span><span class="sxs-lookup"><span data-stu-id="03fff-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="03fff-149">Além disso, o caminho para o keytool depende do local em que você instala o JDK.</span><span class="sxs-lookup"><span data-stu-id="03fff-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="03fff-150">Para saber mais, confira [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] (Ferramenta de gerenciamento de chaves e certificados – keytool) nos documentos online do Java.</span><span class="sxs-lookup"><span data-stu-id="03fff-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="03fff-151">Para criar o arquivo .pfx:</span><span class="sxs-lookup"><span data-stu-id="03fff-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="03fff-152">Para criar o arquivo .cer:</span><span class="sxs-lookup"><span data-stu-id="03fff-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="03fff-153">onde:</span><span class="sxs-lookup"><span data-stu-id="03fff-153">where:</span></span>

* <span data-ttu-id="03fff-154">`<java-install-dir>` é o caminho para o diretório no qual você instalou o Java.</span><span class="sxs-lookup"><span data-stu-id="03fff-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="03fff-155">`<keystore-id>` é o identificador de entrada de armazenamento de chaves (por exemplo, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="03fff-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="03fff-156">`<cert-store-dir>` é o caminho para o diretório no qual você deseja armazenar certificados (por exemplo, `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="03fff-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="03fff-157">`<cert-file-name>` é o nome do arquivo do certificado (por exemplo, `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="03fff-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="03fff-158">`<password>` é a senha que você escolher por proteger o certificado; ela deve ter pelo menos 6 caracteres.</span><span class="sxs-lookup"><span data-stu-id="03fff-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="03fff-159">Embora isso não seja recomendado, você optar por não inserir nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="03fff-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="03fff-160">`<dname>` é o Nome Diferenciado X.500 a ser associado com o alias, e é usado como os campos “emissor” e “assunto” no certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="03fff-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="03fff-161">Para saber mais, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="03fff-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="03fff-162">Carregar o certificado</span><span class="sxs-lookup"><span data-stu-id="03fff-162">Upload the certificate</span></span>
<span data-ttu-id="03fff-163">Para carregar um certificado autoassinado para o Azure, vá para a página **Configurações** no portal clássico, então clique na guia **Certificados de Gerenciamento**. Clique em **Carregar** na parte inferior da página e navegue até o local do arquivo CER que você criou.</span><span class="sxs-lookup"><span data-stu-id="03fff-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="03fff-164">Converter o arquivo PFX em JKS</span><span class="sxs-lookup"><span data-stu-id="03fff-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="03fff-165">No Prompt de comando do Windows (executando como administrador), vá até o diretório que contém os certificados e execute o comando a seguir, em que `<java-install-dir>` é o diretório em que você instalou o Java em seu computador:</span><span class="sxs-lookup"><span data-stu-id="03fff-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="03fff-166">Quando solicitado, digite a senha de chave de armazenamento de destino; esta será a senha para o arquivo JKS.</span><span class="sxs-lookup"><span data-stu-id="03fff-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="03fff-167">Quando solicitado, digite a senha da chave de armazenamento de origem; esta é a senha que você especificou para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="03fff-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="03fff-168">As duas senhas não precisam ser iguais.</span><span class="sxs-lookup"><span data-stu-id="03fff-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="03fff-169">Embora isso não seja recomendado, você optar por não inserir nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="03fff-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="03fff-170">Compilar um aplicativo de criação de aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="03fff-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="03fff-171">Criar o espaço de trabalho do Eclipse e o projeto Maven</span><span class="sxs-lookup"><span data-stu-id="03fff-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="03fff-172">Nesta seção, você cria um espaço de trabalho e um projeto Maven para o aplicativo de criação de aplicativos Web, chamado AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="03fff-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="03fff-173">Crie um novo projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="03fff-173">Create a new Maven project.</span></span> <span data-ttu-id="03fff-174">Clique em **Arquivo > Novo > Projeto Maven**.</span><span class="sxs-lookup"><span data-stu-id="03fff-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="03fff-175">Em **Novo Projeto Maven**, selecione **Criar um projeto simples** e **Usar local padrão de espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="03fff-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="03fff-176">Na segunda página do **Novo Projeto Maven**, especifique o seguinte:</span><span class="sxs-lookup"><span data-stu-id="03fff-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="03fff-177">ID do Grupo: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="03fff-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="03fff-178">ID do Artefato: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="03fff-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="03fff-179">Versão: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="03fff-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="03fff-180">Empacotamento: jar</span><span class="sxs-lookup"><span data-stu-id="03fff-180">Packaging: jar</span></span>
   * <span data-ttu-id="03fff-181">Nome: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="03fff-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="03fff-182">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-182">Click **Finish**.</span></span>
3. <span data-ttu-id="03fff-183">Abra o arquivo pom.xml do novo projeto no Gerenciador de Projetos.</span><span class="sxs-lookup"><span data-stu-id="03fff-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="03fff-184">Selecione a guia **Dependências** . Já que esse é um novo projeto, nenhum pacote está listado ainda.</span><span class="sxs-lookup"><span data-stu-id="03fff-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="03fff-185">Abra a exibição Repositórios Maven.</span><span class="sxs-lookup"><span data-stu-id="03fff-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="03fff-186">**Clique em Janela > Mostrar Exibição > Outros > Maven > Repositórios Maven** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03fff-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="03fff-187">A exibição **Repositórios Maven** aparecerá na parte inferior do IDE.</span><span class="sxs-lookup"><span data-stu-id="03fff-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="03fff-188">Abra **repositórios globais**, clique com o botão direito do mouse no repositório **central** e selecione **Recompilar Índice**.</span><span class="sxs-lookup"><span data-stu-id="03fff-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="03fff-189">Esta etapa pode levar vários minutos dependendo da velocidade da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="03fff-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="03fff-190">Quando o índice for recompilado, você deverá ver os pacotes do Microsoft Azure no Repositório Maven **central** .</span><span class="sxs-lookup"><span data-stu-id="03fff-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="03fff-191">Em **Dependências**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="03fff-192">Em **Inserir ID do Grupo...**, digite `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="03fff-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="03fff-193">Selecione os pacotes de gerenciamento base e gerenciamento de Aplicativos Web do Serviço de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="03fff-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="03fff-194">**Observação:** se você estiver atualizando as dependências após o lançamento de uma nova versão, você precisa adicionar novamente cada uma das dependências nessa lista.</span><span class="sxs-lookup"><span data-stu-id="03fff-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="03fff-195">Depois que você clicar em **Adicionar** e selecionar cada dependência, ela será exibida com o novo número de versão na lista de **Dependências**.</span><span class="sxs-lookup"><span data-stu-id="03fff-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="03fff-196">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03fff-196">Click **OK**.</span></span> <span data-ttu-id="03fff-197">Os pacotes do Azure aparecem na lista de **Dependências** .</span><span class="sxs-lookup"><span data-stu-id="03fff-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="03fff-198">Escrever código Java para criar um aplicativo Web chamando o SDK do Azure</span><span class="sxs-lookup"><span data-stu-id="03fff-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="03fff-199">Em seguida, escreva o código que chama as APIs no SDK do Azure para Java para criar o aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fff-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="03fff-200">Crie uma classe Java para conter o código de ponto de entrada principal.</span><span class="sxs-lookup"><span data-stu-id="03fff-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="03fff-201">No Gerenciador de Projetos, clique com botão direito do mouse no nó do projeto e selecione **Novo > Classe**.</span><span class="sxs-lookup"><span data-stu-id="03fff-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="03fff-202">Em **Nova Classe Java**, nomeie a classe `WebCreator` e marque a caixa de seleção **public static void main**.</span><span class="sxs-lookup"><span data-stu-id="03fff-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="03fff-203">As seleções devem aparecer da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="03fff-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="03fff-204">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-204">Click **Finish**.</span></span> <span data-ttu-id="03fff-205">O arquivo WebCreator.java aparece no Gerenciador de Projetos.</span><span class="sxs-lookup"><span data-stu-id="03fff-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="03fff-206">Chamar a API do Azure para criar um aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="03fff-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="03fff-207">Adicionar as importações necessárias</span><span class="sxs-lookup"><span data-stu-id="03fff-207">Add necessary imports</span></span>
<span data-ttu-id="03fff-208">Em WebCreator.java, adicione as importações a seguir; essas importações fornecem acesso a classes nas bibliotecas de gerenciamento para o consumo de APIs do Azure:</span><span class="sxs-lookup"><span data-stu-id="03fff-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="03fff-209">Definir a classe de ponto de entrada principal</span><span class="sxs-lookup"><span data-stu-id="03fff-209">Define the main entry point class</span></span>
<span data-ttu-id="03fff-210">Como a finalidade do aplicativo AzureWebDemo é criar um aplicativo Web do Serviço de Aplicativo, nomeie a classe principal para esse aplicativo como `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="03fff-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="03fff-211">Essa classe fornece o código de ponto de entrada principal que chama a API de gerenciamento de serviços do Azure para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="03fff-212">Adicione as seguintes definições de parâmetro para o aplicativo Web e espaço Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="03fff-213">Você precisará fornecer suas próprias informações de certificado e ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="03fff-214">onde:</span><span class="sxs-lookup"><span data-stu-id="03fff-214">where:</span></span>

* <span data-ttu-id="03fff-215">`<subscription-id>` é a ID da assinatura do Azure na qual você deseja criar o recurso.</span><span class="sxs-lookup"><span data-stu-id="03fff-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="03fff-216">`<certificate-store-path>` é o caminho e o nome do arquivo para o arquivo JKS em seu diretório de repositório de certificados local.</span><span class="sxs-lookup"><span data-stu-id="03fff-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="03fff-217">Por exemplo, `C:/Certificates/CertificateName.jks` para Linux e `C:\Certificates\CertificateName.jks` para Windows.</span><span class="sxs-lookup"><span data-stu-id="03fff-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="03fff-218">`<certificate-password>` é a senha que você especificou quando criou seu certificado JKS.</span><span class="sxs-lookup"><span data-stu-id="03fff-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="03fff-219">`webAppName` pode ser qualquer nome que você escolher; este procedimento usa o nome `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="03fff-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="03fff-220">O nome de domínio completo é o `webAppName` com o `domainName` anexado, portanto, nesse caso o domínio completo é `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="03fff-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="03fff-221">`domainName` deve ser especificado conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="03fff-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="03fff-222">`webSpaceName` deve ser um dos valores definidos na classe [WebSpaceNames][WebSpaceNames].</span><span class="sxs-lookup"><span data-stu-id="03fff-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="03fff-223">`appServicePlanName` deve ser especificado conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="03fff-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="03fff-224">**Observação:** cada vez que você executa esse aplicativo, precisa alterar o valor de `webAppName` e `appServicePlanName` (ou excluir o aplicativo Web no Portal do Azure) antes de executar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="03fff-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="03fff-225">Caso contrário, a execução falhará porque o mesmo recurso já existe no Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="03fff-226">Definir o método de criação na Web</span><span class="sxs-lookup"><span data-stu-id="03fff-226">Define the web creation method</span></span>
<span data-ttu-id="03fff-227">Em seguida, defina um método para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="03fff-228">Esse método, `createWebApp`, especifica os parâmetros do aplicativo Web e espaço Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="03fff-229">Ele também cria e configura o cliente de gerenciamento de Aplicativos Web do Serviço de Aplicativo, que é definido pelo objeto [WebSiteManagementClient][WebSiteManagementClient].</span><span class="sxs-lookup"><span data-stu-id="03fff-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="03fff-230">O cliente de gerenciamento é essencial para a criação de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="03fff-231">Ele fornece serviços Web RESTful, que permitem que aplicativos gerenciem aplicativos Web (executando operações como criação, atualização e exclusão) chamando a API de gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="03fff-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="03fff-232">O código produzirá como saída o status HTTP da resposta, indicando êxito ou falha e, se for bem-sucedido, retornará o nome do aplicativo Web criado.</span><span class="sxs-lookup"><span data-stu-id="03fff-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="03fff-233">Definir o método main()</span><span class="sxs-lookup"><span data-stu-id="03fff-233">Define the main() method</span></span>
<span data-ttu-id="03fff-234">Forneça o código do método Main () que chama createWebApp() para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="03fff-235">Finalmente, chame `createWebApp` em `main`:</span><span class="sxs-lookup"><span data-stu-id="03fff-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="03fff-236">Executar o aplicativo e verifique a criação de aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="03fff-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="03fff-237">Para verificar se seu aplicativo é executado, clique em **Executar > Executar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="03fff-238">Quando a execução do aplicativo for concluída, você verá a seguinte saída no console do Eclipse:</span><span class="sxs-lookup"><span data-stu-id="03fff-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="03fff-239">Faça logon no portal clássico do Azure e clique em **Aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="03fff-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="03fff-240">O novo aplicativo Web deve aparecer na lista de Aplicativos Web em alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="03fff-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="03fff-241">Implantando um aplicativo para o Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="03fff-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="03fff-242">Depois que você executou AzureWebDemo e criou um novo aplicativo Web, faça logon no portal clássico, clique em **Aplicativos Web**e selecione **WebDemoWebApp** in the **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="03fff-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="03fff-243">Na página do painel do aplicativo Web, clique em **Procurar** (ou clique na URL `webdemowebapp.azurewebsites.net`) para navegar até ele.</span><span class="sxs-lookup"><span data-stu-id="03fff-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="03fff-244">Você verá uma página de alocador de espaço em branco, pois nenhum conteúdo foi publicado ainda para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="03fff-245">Em seguida, você criará um aplicativo "Olá Mundo" e implantá-lo para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="03fff-246">Criar um aplicativo Olá Mundo</span><span class="sxs-lookup"><span data-stu-id="03fff-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="03fff-247">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="03fff-247">Create the application</span></span>
<span data-ttu-id="03fff-248">Para demonstrar como implantar um aplicativo para a Web, o procedimento a seguir mostra como criar um aplicativo Java "Olá Mundo" simples e carregá-lo para o aplicativo Web do Serviço de Aplicativo que o seu aplicativo criou.</span><span class="sxs-lookup"><span data-stu-id="03fff-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="03fff-249">Clique em **Arquivo > Novo > Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="03fff-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="03fff-250">Nomeie-o `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="03fff-250">Name it `JSPHello`.</span></span> <span data-ttu-id="03fff-251">Você não precisa alterar nenhuma outra configuração nesta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="03fff-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="03fff-252">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="03fff-253">No Gerenciador de Projetos, expanda o projeto **JSPHello**, clique com botão direito do mouse em **WebContent** e clique em **Novo > Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="03fff-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="03fff-254">Na caixa de diálogo Novo Arquivo JSP, nomeie o arquivo `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="03fff-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="03fff-255">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-255">Click **Next**.</span></span>
3. <span data-ttu-id="03fff-256">Na caixa de diálogo **Selecionar Modelo JSP**, selecione **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="03fff-257">No index.jsp, adicione o seguinte código nas seções de marca `<head>` e `<body>`:</span><span class="sxs-lookup"><span data-stu-id="03fff-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="03fff-258">Executar o aplicativo Olá Mundo no localhost</span><span class="sxs-lookup"><span data-stu-id="03fff-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="03fff-259">Antes de executar este aplicativo, você precisa configurar algumas propriedades.</span><span class="sxs-lookup"><span data-stu-id="03fff-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="03fff-260">Clique com o botão direito do mouse no projeto **JSPHello** e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="03fff-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="03fff-261">Na caixa de diálogo **Propriedades**: selecione **Caminho de Compilação de Java**, selecione a guia **Ordenar e Exportar**, marque a opção **Biblioteca do Sistema JRE** e clique em **Subir** para movê-lo até o topo da lista.</span><span class="sxs-lookup"><span data-stu-id="03fff-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="03fff-262">Também na caixa de diálogo **Propriedades**: selecione **Tempos de Execução Direcionados** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="03fff-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="03fff-263">Na caixa de diálogo **Novo Ambiente de Tempo de Execução do Servidor**, selecione um servidor como o **Apache Tomcat v7.0** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="03fff-264">Na caixa de diálogo **Servidor Tomcat**, defina **Nome** como `Apache Tomcat v7.0` e defina **Diretório de Instalação do Tomcat** para o diretório no qual você instalou a versão de servidor Tomcat que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="03fff-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="03fff-265">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-265">Click **Finish**.</span></span>
5. <span data-ttu-id="03fff-266">Você retorna então à página **Tempos de Execução Direcionados** da caixa de diálogo **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="03fff-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="03fff-267">Selecione **Apache Tomcat v7.0** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03fff-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="03fff-268">No menu **Executar** do Eclipse, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="03fff-269">Na caixa de diálogo **Executar Como**, selecione **Executar no Servidor**.</span><span class="sxs-lookup"><span data-stu-id="03fff-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="03fff-270">Na caixa de diálogo **Executar no Servidor**, selecione **Servidor Tomcat v7.0**:</span><span class="sxs-lookup"><span data-stu-id="03fff-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="03fff-271">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="03fff-271">Click **Finish**.</span></span>
7. <span data-ttu-id="03fff-272">Quando o aplicativo for executado, você deverá ver a página **JSPHello** em uma janela de localhost no Eclipse (`http://localhost:8080/JSPHello/`), exibindo a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="03fff-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="03fff-273">Exportar seu aplicativo como um WAR (arquivo da Web)</span><span class="sxs-lookup"><span data-stu-id="03fff-273">Export the application as a WAR</span></span>
<span data-ttu-id="03fff-274">Exporte os arquivos de projeto Web como um WAR (arquivo Web) para implantá-lo para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="03fff-275">Os seguintes arquivos de projeto Web residem na pasta WebContent:</span><span class="sxs-lookup"><span data-stu-id="03fff-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="03fff-276">Clique na pasta WebContent e selecione **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="03fff-277">Na caixa de diálogo **Selecionar Exportação**, clique no arquivo **Web > WAR** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="03fff-278">Na caixa de diálogo **Exportar WAR** , selecione o diretório de origem no projeto atual e inclua o nome do arquivo WAR no final.</span><span class="sxs-lookup"><span data-stu-id="03fff-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="03fff-279">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03fff-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="03fff-280">Para obter mais informações sobre como implantar arquivos WAR, consulte [Adicionar um aplicativo Java a Aplicativos Web do Serviço de Aplicativo do Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="03fff-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="03fff-281">Implantação do aplicativo Olá Mundo usando FTP</span><span class="sxs-lookup"><span data-stu-id="03fff-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="03fff-282">Selecione um cliente FTP de terceiros para publicar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fff-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="03fff-283">Este procedimento descreve duas opções: o console Kudu integrado ao Azure e o FileZilla, uma ferramenta conhecida com uma interface do usuário gráfica e prática.</span><span class="sxs-lookup"><span data-stu-id="03fff-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="03fff-284">**Observação:** o kit de ferramentas do Azure para Eclipse dá suporte à implantação de contas de armazenamento e serviços de nuvem, mas não dá suporte à implantação de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="03fff-285">Você pode implantar contas de armazenamento e serviços de nuvem usando um projeto de implantação do Azure conforme descrito em [Criando um Aplicativo Olá Mundo do Azure no Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mas não para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="03fff-286">Use outros métodos como FTP ou GitHub para transferir arquivos para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="03fff-287">**Observação:** não é recomendável usar FTP no prompt de comando do Windows (o utilitário de linha de comando FTP.EXE que acompanha o Windows).</span><span class="sxs-lookup"><span data-stu-id="03fff-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="03fff-288">Os clientes FTP que usam FTP ativo, como FTP.EXE, muitas vezes não funcionam através de firewalls.</span><span class="sxs-lookup"><span data-stu-id="03fff-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="03fff-289">O FTP ativo especifica um endereço interno baseado em LAN, ao qual a conexão por meio de um servidor FTP provavelmente falhará.</span><span class="sxs-lookup"><span data-stu-id="03fff-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="03fff-290">Para obter mais informações sobre a implantação de um aplicativo Web de Serviço de Aplicativo usando o FTP, consulte os tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="03fff-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="03fff-291">Implantar usando um utilitário FTP</span><span class="sxs-lookup"><span data-stu-id="03fff-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="03fff-292">Configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="03fff-292">Set up deployment credentials</span></span>
<span data-ttu-id="03fff-293">Verifique se você executou o aplicativo **AzureWebDemo** para criar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="03fff-294">Você transferirá arquivos para este local.</span><span class="sxs-lookup"><span data-stu-id="03fff-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="03fff-295">Faça logon no portal clássico e clique em **Aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="03fff-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="03fff-296">Certifique-se de **WebDemoWebApp** aparece na lista de aplicativos Web e certifique-se de que ele esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="03fff-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="03fff-297">Clique em **WebDemoWebApp** para abrir sua página **Painel**.</span><span class="sxs-lookup"><span data-stu-id="03fff-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="03fff-298">Na página **Painel**, em **Visualização rápida**, clique em **Configurar suas credenciais de implantação** (se você já tem credenciais de implantação, isso aparece como **Redefinir suas credenciais de implantação**).</span><span class="sxs-lookup"><span data-stu-id="03fff-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="03fff-299">As credenciais de implantação estão associadas com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03fff-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="03fff-300">Você precisa especificar um nome de usuário e senha que você possa usar para implantar usando Git e FTP.</span><span class="sxs-lookup"><span data-stu-id="03fff-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="03fff-301">Você pode usar essas credenciais para implantar em qualquer aplicativo Web, em todas as assinaturas do Azure associadas à sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03fff-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="03fff-302">Forneça as credenciais de implantação de FTP e Git na caixa de diálogo, e registre o nome de usuário e senha para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="03fff-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="03fff-303">Obter informações de conexão de FTP</span><span class="sxs-lookup"><span data-stu-id="03fff-303">Get FTP connection information</span></span>
<span data-ttu-id="03fff-304">Para usar o FTP para implantar arquivos de aplicativo para o aplicativo Web recém-criado, você precisa obter as informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="03fff-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="03fff-305">Há duas maneiras de obter as informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="03fff-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="03fff-306">Uma maneira é visitar a página **Painel** do aplicativo Web; a outra maneira é baixar o perfil de publicação do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="03fff-307">O perfil de publicação é um arquivo XML que fornece informações como as credenciais de logon e o nome de host FTP para seus aplicativos Web, no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="03fff-308">Você pode usar esse nome de usuário e senha para implantar em qualquer aplicativo Web em todas as assinaturas associadas à conta do Azure, não apenas esta aqui.</span><span class="sxs-lookup"><span data-stu-id="03fff-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="03fff-309">Para saber mais de conexão FTP por meio da folha do aplicativo Web no [portal do Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="03fff-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="03fff-310">Em **Essentials**, localize e copie o **Nome do host FTP**.</span><span class="sxs-lookup"><span data-stu-id="03fff-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="03fff-311">Isso é um URI similar a `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="03fff-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="03fff-312">Em **Essentials**, localize e copie o **nome de usuário de implantação/FTP**.</span><span class="sxs-lookup"><span data-stu-id="03fff-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="03fff-313">Ele terá o formato *nomedoaplicativoWeb\nomedeusuário-implantação*; por exemplo, `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="03fff-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="03fff-314">Para obter informações de conexão de FTP por meio do perfil de publicação:</span><span class="sxs-lookup"><span data-stu-id="03fff-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="03fff-315">Na folha do aplicativo Web, clique em **Perfil de publicação Get**.</span><span class="sxs-lookup"><span data-stu-id="03fff-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="03fff-316">Isso baixará um arquivo .publishsettings para sua unidade local.</span><span class="sxs-lookup"><span data-stu-id="03fff-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="03fff-317">Abra o arquivo .publishsettings em um editor de XML ou editor de texto e localize o elemento `<publishProfile>` que contém `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="03fff-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="03fff-318">Sua tela deverá ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="03fff-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="03fff-319">Observe que as configurações `publishProfile` do aplicativo Web são mapeadas para as configurações do Gerenciador de Sites FileZilla da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="03fff-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="03fff-320">`publishUrl` é o mesmo que **nome do host FTP**, o valor que você definiu em **Host**.</span><span class="sxs-lookup"><span data-stu-id="03fff-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="03fff-321">`publishMethod="FTP"` significa que você define **Protocolo** como **FTP - Protocolo de Transferência de Arquivos** e **Criptografia** como **Usar FTP simples**.</span><span class="sxs-lookup"><span data-stu-id="03fff-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="03fff-322">`userName` e `userPWD` são as chaves para os valores de nome de usuário e senha reais especificados quando você redefine as credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="03fff-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="03fff-323">`userName` é o mesmo que **Implantação/usuário de FTP**.</span><span class="sxs-lookup"><span data-stu-id="03fff-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="03fff-324">Elas são mapeadas para **Usuário** e **Senha** no FileZilla.</span><span class="sxs-lookup"><span data-stu-id="03fff-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="03fff-325">`ftpPassiveMode="True"` significa que o site FTP usa transferência por FTP passiva; selecione **Passiva** on the **Configurações de Transferência** .</span><span class="sxs-lookup"><span data-stu-id="03fff-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="03fff-326">Configurar o aplicativo Web para hospedar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="03fff-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="03fff-327">Antes de publicar o aplicativo, você precisa alterar algumas configurações para que o aplicativo Web possa hospedar um aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="03fff-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="03fff-328">No portal clássico, vá para a página **Painel** do aplicativo Web e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="03fff-329">Na página **Configurar** , especifique as configurações a seguir.</span><span class="sxs-lookup"><span data-stu-id="03fff-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="03fff-330">Em **Versão do Java**, o padrão é **Desativado**; selecione a versão de Java que seu aplicativo busca; por exemplo, 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="03fff-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="03fff-331">Depois de fazer isso, verifique também que **Contêiner da Web** esteja definido para uma versão do Servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="03fff-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="03fff-332">Em **Documentos Padrão**, adicione index.jsp e mova-o para a parte superior da lista.</span><span class="sxs-lookup"><span data-stu-id="03fff-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="03fff-333">(O arquivo padrão para aplicativos Web é hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="03fff-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="03fff-334">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="03fff-335">Publicar seu aplicativo usando Kudu</span><span class="sxs-lookup"><span data-stu-id="03fff-335">Publish your application using Kudu</span></span>
<span data-ttu-id="03fff-336">Uma maneira de publicar o aplicativo é usar o console de depuração Kudu integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="03fff-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="03fff-337">O Kudu é conhecido por ser estável e consistente com Aplicativos Web do Serviço de Aplicativo e servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="03fff-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="03fff-338">Você pode acessar o console para o aplicativo Web navegando até uma URL no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="03fff-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="03fff-339">Neste procedimento, o console Kudu está localizado na URL a seguir; navegue até o local:</span><span class="sxs-lookup"><span data-stu-id="03fff-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="03fff-340">No menu superior, selecione **Console de Depuração > CMD**.</span><span class="sxs-lookup"><span data-stu-id="03fff-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="03fff-341">Na linha de comando do console, navegue até `/site/wwwroot` (ou clique em `site`, depois em `wwwroot` na exibição do diretório, na parte superior da página):</span><span class="sxs-lookup"><span data-stu-id="03fff-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="03fff-342">Depois de especificar a **Versão do Java**, o servidor Tomcat deve criar uma pasta webapps.</span><span class="sxs-lookup"><span data-stu-id="03fff-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="03fff-343">Na linha de comando de console, navegue até a pasta webapps:</span><span class="sxs-lookup"><span data-stu-id="03fff-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="03fff-344">Arraste JSPHello.war em `<project-path>/JSPHello/src/` e solte-o no modo de exibição de pasta do Kudu em `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="03fff-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="03fff-345">Não arraste-o para a área "Arraste aqui para carregar e compactar", porque o Tomcat vai descompactá-lo.</span><span class="sxs-lookup"><span data-stu-id="03fff-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="03fff-346">Primeiro, o JSPHello.war aparece na área da pasta sozinho:</span><span class="sxs-lookup"><span data-stu-id="03fff-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="03fff-347">Em um curto período de tempo (provavelmente menos de 5 minutos), o servidor Tomcat descompactará o arquivo WAR em um diretório JSPHello.</span><span class="sxs-lookup"><span data-stu-id="03fff-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="03fff-348">Clique no diretório raiz para ver se index.jsp foi descompactado e copiado para esse local.</span><span class="sxs-lookup"><span data-stu-id="03fff-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="03fff-349">Se isso ocorreu, navegue até a pasta webapps para ver se a pasta JSPHello descompactada foi criado ou não.</span><span class="sxs-lookup"><span data-stu-id="03fff-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="03fff-350">Se você não ver esses itens, aguarde e repita.</span><span class="sxs-lookup"><span data-stu-id="03fff-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="03fff-351">Publicar seu aplicativo usando o FileZilla (opcional)</span><span class="sxs-lookup"><span data-stu-id="03fff-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="03fff-352">Outra ferramenta que você pode usar para publicar o aplicativo é o FileZilla, um cliente FTP de terceiros popular, com uma interface do usuário gráfica e prática.</span><span class="sxs-lookup"><span data-stu-id="03fff-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="03fff-353">Você pode baixar e instalar o FileZilla de [http://filezilla-project.org/](http://filezilla-project.org/) se você ainda não o tiver.</span><span class="sxs-lookup"><span data-stu-id="03fff-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="03fff-354">Para obter mais informações sobre como usar o cliente, confira a [Documentação do FileZilla](https://wiki.filezilla-project.org/Documentation) e esta entrada de blog em [Clientes FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="03fff-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="03fff-355">No FileZilla, clique em **Arquivo > Gerenciador de Sites**.</span><span class="sxs-lookup"><span data-stu-id="03fff-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="03fff-356">Na caixa de diálogo **Gerenciador de Sites**, clique em **Novo Site**.</span><span class="sxs-lookup"><span data-stu-id="03fff-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="03fff-357">Um novo site FTP em branco aparecerá em **Selecionar Entrada** , solicitando que você forneça um nome.</span><span class="sxs-lookup"><span data-stu-id="03fff-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="03fff-358">Para este procedimento, nomeie-o como `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="03fff-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="03fff-359">Na guia **Geral** , especifique as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="03fff-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="03fff-360">**Host:** insira o **Nome de Host do FTP** que você copiou do painel.</span><span class="sxs-lookup"><span data-stu-id="03fff-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="03fff-361">**Porta:** (deixe isso em branco, já que se trata de uma transferência passiva e o servidor determinará a porta a ser usada.)</span><span class="sxs-lookup"><span data-stu-id="03fff-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="03fff-362">**Protocolo:** protocolo FTP</span><span class="sxs-lookup"><span data-stu-id="03fff-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="03fff-363">**Criptografia:** usar FTP simples</span><span class="sxs-lookup"><span data-stu-id="03fff-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="03fff-364">**Tipo de Logon:** normal</span><span class="sxs-lookup"><span data-stu-id="03fff-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="03fff-365">**Usuário:** insira o usuário de implantação/FTP que você copiou do painel.</span><span class="sxs-lookup"><span data-stu-id="03fff-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="03fff-366">Esse é o nome de usuário de FTP completo, que tem o formato *nomedoaplicativoweb\nomedeusuário*.</span><span class="sxs-lookup"><span data-stu-id="03fff-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="03fff-367">**Senha:** insira a senha especificada ao definir as credenciais da implantação.</span><span class="sxs-lookup"><span data-stu-id="03fff-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="03fff-368">Na guia **Configurações de Transferência**, selecione **Passiva**.</span><span class="sxs-lookup"><span data-stu-id="03fff-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="03fff-369">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-369">Click **Connect**.</span></span> <span data-ttu-id="03fff-370">Se a conexão for bem-sucedida, o console do FileZilla exibirá uma mensagem `Status: Connected` e emitirá um comando `LIST` para listar o conteúdo da pasta.</span><span class="sxs-lookup"><span data-stu-id="03fff-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="03fff-371">No painel do site **Local** , selecione o diretório de origem no qual reside o arquivo JSPHello.war; o caminho será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="03fff-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="03fff-372">No painel do site **Remoto** , selecione a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="03fff-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="03fff-373">Você implantará o arquivo WAR no diretório `webapps` na raiz do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="03fff-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="03fff-374">Navegue até `/site/wwwroot`, clique com o botão direito do mouse em `wwwroot` e selecione **Criar diretório**.</span><span class="sxs-lookup"><span data-stu-id="03fff-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="03fff-375">Nomeie o diretório como `webapps` e acesse esse diretório.</span><span class="sxs-lookup"><span data-stu-id="03fff-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="03fff-376">Transfira JSPHello.war para `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="03fff-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="03fff-377">Selecione JSPHello.war na lista de arquivos **Local**, clique com botão direito do mouse nele e selecione **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="03fff-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="03fff-378">Você deverá vê-lo aparecer em `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="03fff-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="03fff-379">Depois de copiar JSPHello.war para a pasta webapps, o Servidor Tomcat descompactará automaticamente os arquivos contidos no arquivo WAR.</span><span class="sxs-lookup"><span data-stu-id="03fff-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="03fff-380">Embora o servidor Tomcat comece a desempacotar quase imediatamente, pode levar um longo tempo (possivelmente horas) para que os arquivos sejam exibidos no cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="03fff-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="03fff-381">Executar o aplicativo Olá Mundo no aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="03fff-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="03fff-382">Depois de ter carregado o arquivo WAR e verificado que o servidor Tomcat criou um diretório `JSPHello` descompactado, navegue até `http://webdemowebapp.azurewebsites.net/JSPHello` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fff-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="03fff-383">**Observação:** se clicar em **Procurar** no portal clássico, você poderá obter a página da Web padrão, dizendo "Este aplicativo Web baseado em Java foi criado com êxito."</span><span class="sxs-lookup"><span data-stu-id="03fff-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="03fff-384">Você talvez precise atualizar a página da Web para exibir a saída do aplicativo, em vez da página da Web padrão.</span><span class="sxs-lookup"><span data-stu-id="03fff-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="03fff-385">Quando o aplicativo for executado, você deverá ver uma página da Web com a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="03fff-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="03fff-386">Limpar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="03fff-386">Clean up Azure resources</span></span>
<span data-ttu-id="03fff-387">Este procedimento cria um aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fff-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="03fff-388">Você será cobrado pelo recurso enquanto ele existir.</span><span class="sxs-lookup"><span data-stu-id="03fff-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="03fff-389">A menos que você planeje continuar usando o aplicativo Web para teste ou desenvolvimento, você deve considerar interromper sua execução ou excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="03fff-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="03fff-390">Um aplicativo Web cuja execução foi interrompida ainda incorrerá em um pequeno encargo, mas você poderá reiniciá-lo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="03fff-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="03fff-391">A exclusão de um aplicativo Web apaga todos os dados que você carregou nele.</span><span class="sxs-lookup"><span data-stu-id="03fff-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
