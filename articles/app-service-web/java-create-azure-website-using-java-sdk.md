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
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="24c14-103">Criar um aplicativo Web no serviço de aplicativo do Azure usando Olá SDK do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="24c14-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="24c14-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="24c14-104">Overview</span></span>
<span data-ttu-id="24c14-105">Este passo a passo mostra como toocreate um SDK do Azure para um aplicativo Java que cria um aplicativo Web no [do serviço de aplicativo do Azure][Azure App Service], em seguida, implantar um aplicativo tooit.</span><span class="sxs-lookup"><span data-stu-id="24c14-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="24c14-106">Ele consiste em duas partes:</span><span class="sxs-lookup"><span data-stu-id="24c14-106">It consists of two parts:</span></span>

* <span data-ttu-id="24c14-107">Parte 1 demonstra como toobuild um aplicativo Java que cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="24c14-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="24c14-108">Parte 2 demonstra como toocreate um JSP simple "Alô mundo" aplicativo, em seguida, use um FTP cliente toodeploy código tooApp serviço.</span><span class="sxs-lookup"><span data-stu-id="24c14-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24c14-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24c14-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="24c14-110">Instalações de software</span><span class="sxs-lookup"><span data-stu-id="24c14-110">Software Installations</span></span>
<span data-ttu-id="24c14-111">Olá AzureWebDemo código do aplicativo neste artigo foi escrito usando o Azure Java SDK 0.7.0, que pode ser instalado usando Olá [Web Platform Installer] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="24c14-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="24c14-112">Além disso, certifique-se de que toouse Olá última versão do hello [Kit de ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="24c14-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="24c14-113">Depois de instalar o SDK de hello, atualizar dependências Olá em seu projeto Eclipse executando **Atualizar índice** na **Maven repositórios**, adicionar novamente a versão mais recente de saudação de cada pacote hello  **Dependências** janela.</span><span class="sxs-lookup"><span data-stu-id="24c14-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="24c14-114">Você pode verificar a versão de saudação do software instalado no Eclipse, clicando em **Ajuda > detalhes da instalação**; você deve ter pelo menos Olá seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="24c14-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="24c14-115">Pacote para Bibliotecas do Microsoft Azure para Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="24c14-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="24c14-116">Eclipse IDE para desenvolvedores de Java EE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="24c14-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="24c14-117">Criar e configurar recursos de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="24c14-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="24c14-118">Antes de iniciar este procedimento, você precisa toohave uma assinatura ativa do Azure e configurar um padrão de AD (Active Directory) no Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="24c14-119">Criar um AD (Active Directory) no Azure</span><span class="sxs-lookup"><span data-stu-id="24c14-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="24c14-120">Se você não tiver um Active Directory (AD) em sua assinatura do Azure, faça logon no hello [portal clássico do Azure] [ Azure classic portal] com sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="24c14-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="24c14-121">Se você tiver várias assinaturas, clique em **assinaturas** e selecione saudação padrão diretório para assinatura Olá deseja toouse para este projeto.</span><span class="sxs-lookup"><span data-stu-id="24c14-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="24c14-122">Em seguida, clique em **aplicar** tooswitch toothat exibição da assinatura.</span><span class="sxs-lookup"><span data-stu-id="24c14-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="24c14-123">Selecione **do Active Directory** no menu de saudação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="24c14-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="24c14-124">**Clique em Novo > Diretório > Criação Personalizada**.</span><span class="sxs-lookup"><span data-stu-id="24c14-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="24c14-125">Em **Adicionar Diretório**, selecione **Criar Novo Diretório**.</span><span class="sxs-lookup"><span data-stu-id="24c14-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="24c14-126">Em **Nome**, insira um nome de diretório.</span><span class="sxs-lookup"><span data-stu-id="24c14-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="24c14-127">Em **Domínio**, insira um nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="24c14-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="24c14-128">Este é um nome de domínio básico que está incluído por padrão com seu diretório; ele tem o formato de saudação `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="24c14-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="24c14-129">Você pode nomear com base no nome do diretório hello ou outro nome de domínio que você possui.</span><span class="sxs-lookup"><span data-stu-id="24c14-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="24c14-130">Posteriormente, você pode adicionar outro nome de domínio que sua organização já utilize.</span><span class="sxs-lookup"><span data-stu-id="24c14-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="24c14-131">Em **País ou região**, selecione sua localidade.</span><span class="sxs-lookup"><span data-stu-id="24c14-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="24c14-132">Para saber mais sobre o AD, confira [O que é um diretório do Azure AD][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="24c14-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="24c14-133">Criar um Certificado de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="24c14-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="24c14-134">Olá SDK do Azure para Java usa tooauthenticate de certificados de gerenciamento com assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="24c14-135">Esses são x. 509 v3 certificados que usar tooauthenticate um aplicativo cliente que usa Olá tooact de API de gerenciamento de serviços em nome de recursos de assinatura toomanage do proprietário de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="24c14-136">código de Olá neste procedimento usa um certificado autoassinado tooauthenticate com o Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="24c14-137">Para esse procedimento, você precisa toocreate um certificado e carregá-lo toohello [portal clássico do Azure] [ Azure classic portal] com antecedência.</span><span class="sxs-lookup"><span data-stu-id="24c14-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="24c14-138">Isso envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-138">This involves hello following steps:</span></span>

* <span data-ttu-id="24c14-139">Gere um arquivo PFX que represente seu certificado de cliente e salve-o localmente.</span><span class="sxs-lookup"><span data-stu-id="24c14-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="24c14-140">Gere um certificado de gerenciamento (arquivo CER) do arquivo PFX de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="24c14-141">Carregar Olá CER arquivo tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="24c14-142">Converta o arquivo PFX de saudação em JKS, como Java usa esse tooauthenticate formato usando certificados.</span><span class="sxs-lookup"><span data-stu-id="24c14-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="24c14-143">Grave o código de autenticação do aplicativo hello, que se refere a arquivos JKS local toohello.</span><span class="sxs-lookup"><span data-stu-id="24c14-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="24c14-144">Quando você concluir este procedimento, certificado CER Olá residem em sua assinatura do Azure e certificado JKS Olá residem em sua unidade local.</span><span class="sxs-lookup"><span data-stu-id="24c14-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="24c14-145">Para saber mais sobre gerenciamento de certificados, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="24c14-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="24c14-146">Criar um certificado</span><span class="sxs-lookup"><span data-stu-id="24c14-146">Create a certificate</span></span>
<span data-ttu-id="24c14-147">toocreate seu próprio certificado autoassinado, abra um console de comando em seu sistema operacional e execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="24c14-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="24c14-148">**Observação:** computador Olá no qual você executa este comando deve ter Olá JDK instalado.</span><span class="sxs-lookup"><span data-stu-id="24c14-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="24c14-149">Além disso, Olá caminho toohello keytool depende local Olá em que você instala Olá JDK.</span><span class="sxs-lookup"><span data-stu-id="24c14-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="24c14-150">Para obter mais informações, consulte [chave e a ferramenta de gerenciamento de certificado (keytool)] [ Key and Certificate Management Tool (keytool)] em documentos online do hello Java.</span><span class="sxs-lookup"><span data-stu-id="24c14-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="24c14-151">arquivo do toocreate hello. pfx:</span><span class="sxs-lookup"><span data-stu-id="24c14-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="24c14-152">arquivo. cer Olá toocreate:</span><span class="sxs-lookup"><span data-stu-id="24c14-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="24c14-153">onde:</span><span class="sxs-lookup"><span data-stu-id="24c14-153">where:</span></span>

* <span data-ttu-id="24c14-154">`<java-install-dir>`é Olá caminho toohello diretório no qual você instalou o Java.</span><span class="sxs-lookup"><span data-stu-id="24c14-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="24c14-155">`<keystore-id>`é o identificador de entrada de repositório de chaves de saudação (por exemplo, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="24c14-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="24c14-156">`<cert-store-dir>`é Olá caminho toohello diretório no qual você deseja toostore certificados (por exemplo `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="24c14-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="24c14-157">`<cert-file-name>`é o nome Olá Olá do arquivo de certificado (por exemplo `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="24c14-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="24c14-158">`<password>`senha Olá escolher certificado de saudação tooprotect; ele deve ter pelo menos 6 caracteres.</span><span class="sxs-lookup"><span data-stu-id="24c14-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="24c14-159">Embora isso não seja recomendado, você optar por não inserir nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="24c14-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="24c14-160">`<dname>`é Olá nome diferenciado do x. 500 toobe associada alias e é usado como o emissor hello e campos de entidade no certificado autoassinado hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="24c14-161">Para saber mais, confira [Criar e carregar um certificado de gerenciamento no Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="24c14-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="24c14-162">Carregar certificado Olá</span><span class="sxs-lookup"><span data-stu-id="24c14-162">Upload hello certificate</span></span>
<span data-ttu-id="24c14-163">tooupload tooAzure um certificado autoassinado, vá toohello **configurações** página no portal clássico do hello, clique em Olá **certificados de gerenciamento** guia. Clique em **carregar** final Olá Olá página e navegar toohello local do arquivo CER Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="24c14-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="24c14-164">Converter o arquivo PFX de saudação em JKS</span><span class="sxs-lookup"><span data-stu-id="24c14-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="24c14-165">Saudação de Prompt de comando do Windows (executando como administrador), cd toohello diretório que contém Olá certificados e executado Olá a seguir de comando, onde `<java-install-dir>` é Olá diretório no qual você instalou Java em seu computador:</span><span class="sxs-lookup"><span data-stu-id="24c14-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="24c14-166">Quando solicitado, insira a senha de chave de armazenamento de destino Olá; Essa será a senha Olá para o arquivo JKS hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="24c14-167">Quando solicitado, insira a senha de chave de armazenamento de origem Olá; Esta é Olá senha especificada para o arquivo PFX de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="24c14-168">as duas senhas de saudação não tem toobe Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="24c14-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="24c14-169">Embora isso não seja recomendado, você optar por não inserir nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="24c14-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="24c14-170">Compilar um aplicativo de criação de aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="24c14-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="24c14-171">Criar hello espaço de trabalho do Eclipse e projeto Maven</span><span class="sxs-lookup"><span data-stu-id="24c14-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="24c14-172">Nesta seção, você criará um espaço de trabalho e um projeto Maven para o aplicativo para criação de aplicativos do web hello, denominado AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="24c14-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="24c14-173">Crie um novo projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="24c14-173">Create a new Maven project.</span></span> <span data-ttu-id="24c14-174">Clique em **Arquivo > Novo > Projeto Maven**.</span><span class="sxs-lookup"><span data-stu-id="24c14-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="24c14-175">Em **Novo Projeto Maven**, selecione **Criar um projeto simples** e **Usar local padrão de espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="24c14-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="24c14-176">Na segunda página de saudação do **novo projeto Maven**, especifique Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="24c14-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="24c14-177">ID do Grupo: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="24c14-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="24c14-178">ID do Artefato: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="24c14-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="24c14-179">Versão: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="24c14-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="24c14-180">Empacotamento: jar</span><span class="sxs-lookup"><span data-stu-id="24c14-180">Packaging: jar</span></span>
   * <span data-ttu-id="24c14-181">Nome: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="24c14-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="24c14-182">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-182">Click **Finish**.</span></span>
3. <span data-ttu-id="24c14-183">Abra o arquivo de pom.xml de saudação do novo projeto no Explorador de projeto.</span><span class="sxs-lookup"><span data-stu-id="24c14-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="24c14-184">Selecione Olá **dependências** guia. Já que esse é um novo projeto, nenhum pacote está listado ainda.</span><span class="sxs-lookup"><span data-stu-id="24c14-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="24c14-185">Exibir hello abrir Maven repositórios.</span><span class="sxs-lookup"><span data-stu-id="24c14-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="24c14-186">**Clique em Janela > Mostrar Exibição > Outros > Maven > Repositórios Maven** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="24c14-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="24c14-187">Olá **Maven repositórios** exibição aparecerá na parte inferior de saudação do hello IDE.</span><span class="sxs-lookup"><span data-stu-id="24c14-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="24c14-188">Abra **repositórios Global**, Olá do botão direito do mouse **central** repositório e selecione **recriar índice**.</span><span class="sxs-lookup"><span data-stu-id="24c14-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="24c14-189">Esta etapa pode levar vários minutos dependendo da velocidade da saudação de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="24c14-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="24c14-190">Quando recriações de índice hello, você verá pacotes Microsoft Azure Olá Olá **central** Repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="24c14-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="24c14-191">Em **Dependências**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="24c14-192">Em **Inserir ID do Grupo...**, digite `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="24c14-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="24c14-193">Selecione os pacotes de saudação para gerenciamento de base e o gerenciamento de serviço de aplicativo Web de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="24c14-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="24c14-194">**Observação:** se você estiver atualizando dependências Olá após uma nova versão, você precisa toore-adicionar cada uma das dependências de saudação nesta lista.</span><span class="sxs-lookup"><span data-stu-id="24c14-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="24c14-195">Depois de clicar em **adicionar** e selecione cada dependência, ela será exibida com o novo número de versão Olá no hello **dependências** lista.</span><span class="sxs-lookup"><span data-stu-id="24c14-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="24c14-196">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="24c14-196">Click **OK**.</span></span> <span data-ttu-id="24c14-197">Olá pacotes do Azure e aparecem em Olá **dependências** lista.</span><span class="sxs-lookup"><span data-stu-id="24c14-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="24c14-198">Escrevendo código Java tooCreate um aplicativo Web por saudação da chamada do SDK do Azure</span><span class="sxs-lookup"><span data-stu-id="24c14-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="24c14-199">Em seguida, escreva um código de saudação que chama as APIs no SDK do Azure de saudação de saudação do Java toocreate aplicativo do serviço de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="24c14-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="24c14-200">Crie um código de ponto de entrada principal Java classe toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="24c14-201">No Explorador de projeto, clique com botão direito no nó do projeto hello e selecione **Novo > classe**.</span><span class="sxs-lookup"><span data-stu-id="24c14-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="24c14-202">Em **nova classe Java**, nomeie a classe Olá `WebCreator` e verifique Olá **público estático anulado main** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="24c14-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="24c14-203">seleções de saudação devem aparecer da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="24c14-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="24c14-204">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-204">Click **Finish**.</span></span> <span data-ttu-id="24c14-205">arquivo de WebCreator.java Olá aparece no Explorador de projeto.</span><span class="sxs-lookup"><span data-stu-id="24c14-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="24c14-206">Olá tooCreate de API do Azure ao chamar um serviço de aplicativo de um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="24c14-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="24c14-207">Adicionar as importações necessárias</span><span class="sxs-lookup"><span data-stu-id="24c14-207">Add necessary imports</span></span>
<span data-ttu-id="24c14-208">Em WebCreator.java, adicione Olá a seguir importa; Esses importações fornecem acesso tooclasses em Olá bibliotecas de gerenciamento para o consumo de APIs do Azure:</span><span class="sxs-lookup"><span data-stu-id="24c14-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="24c14-209">Definir a classe de ponto de entrada principal Olá</span><span class="sxs-lookup"><span data-stu-id="24c14-209">Define hello main entry point class</span></span>
<span data-ttu-id="24c14-210">Como objetivo Olá Olá AzureWebDemo aplicativo é toocreate um serviço de aplicativo de um aplicativo Web, nome de classe principal Olá para este aplicativo `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="24c14-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="24c14-211">Essa classe fornece código de ponto de entrada principal Olá que chama Olá API de gerenciamento de serviços do Azure toocreate Olá web app.</span><span class="sxs-lookup"><span data-stu-id="24c14-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="24c14-212">Adicione Olá definições de parâmetro para Olá web app e o espaço da Web a seguir.</span><span class="sxs-lookup"><span data-stu-id="24c14-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="24c14-213">Você precisará tooprovide suas próprias informações de ID e o certificado de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="24c14-214">onde:</span><span class="sxs-lookup"><span data-stu-id="24c14-214">where:</span></span>

* <span data-ttu-id="24c14-215">`<subscription-id>`é Olá ID de assinatura do Azure no qual você deseja que o recurso de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="24c14-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="24c14-216">`<certificate-store-path>`é Olá caminho e nome de arquivo toohello JKS arquivo em seu diretório de repositório de certificados local.</span><span class="sxs-lookup"><span data-stu-id="24c14-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="24c14-217">Por exemplo, `C:/Certificates/CertificateName.jks` para Linux e `C:\Certificates\CertificateName.jks` para Windows.</span><span class="sxs-lookup"><span data-stu-id="24c14-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="24c14-218">`<certificate-password>`é a senha de saudação que você especificou quando criou seu certificado JKS.</span><span class="sxs-lookup"><span data-stu-id="24c14-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="24c14-219">`webAppName`pode ser qualquer nome que você escolher; Este procedimento usa o nome da saudação `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="24c14-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="24c14-220">o nome de domínio completo Olá é hello `webAppName` com hello `domainName` anexado, portanto nesse caso domínio completo Olá é `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="24c14-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="24c14-221">`domainName` deve ser especificado conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="24c14-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="24c14-222">`webSpaceName`deve ser um dos valores de saudação definidos no hello [WebSpaceNames] [ WebSpaceNames] classe.</span><span class="sxs-lookup"><span data-stu-id="24c14-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="24c14-223">`appServicePlanName` deve ser especificado conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="24c14-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="24c14-224">**Observação:** sempre executar este aplicativo, você precisa toochange Olá valor de `webAppName` e `appServicePlanName` (ou excluir Olá web app no hello Portal do Azure) antes de executar o aplicativo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="24c14-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="24c14-225">Caso contrário, a execução falhará porque hello mesmo recurso já existe no Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="24c14-226">Definir o método de criação de web hello</span><span class="sxs-lookup"><span data-stu-id="24c14-226">Define hello web creation method</span></span>
<span data-ttu-id="24c14-227">Em seguida, defina um aplicativo web do método toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="24c14-228">Esse método, `createWebApp`, especifica os parâmetros de saudação do Olá web app e Olá espaço na Web.</span><span class="sxs-lookup"><span data-stu-id="24c14-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="24c14-229">Ele também cria e configura o cliente de gerenciamento de aplicativos de Web do serviço de aplicativo hello, que é definido como Olá [WebSiteManagementClient] [ WebSiteManagementClient] objeto.</span><span class="sxs-lookup"><span data-stu-id="24c14-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="24c14-230">cliente de gerenciamento de saudação é chave toocreating os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="24c14-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="24c14-231">Ele fornece os serviços web RESTful que permitem que aplicativos toomanage aplicativos web (executando operações como criar, atualizar e excluir) ao chamar a API de gerenciamento do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

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

<span data-ttu-id="24c14-232">código de Olá mostrará o status HTTP de saudação da resposta Olá indicando êxito ou falha e se for bem-sucedido, produzirá o nome de saudação do hello criado o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="24c14-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="24c14-233">Definir o método Main () de saudação</span><span class="sxs-lookup"><span data-stu-id="24c14-233">Define hello main() method</span></span>
<span data-ttu-id="24c14-234">Fornece o código do método Main Olá esse aplicativo de web chamadas createWebApp() toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="24c14-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="24c14-235">Finalmente, chame `createWebApp` em `main`:</span><span class="sxs-lookup"><span data-stu-id="24c14-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="24c14-236">Executar o aplicativo hello e verifique se a criação do aplicativo web</span><span class="sxs-lookup"><span data-stu-id="24c14-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="24c14-237">tooverify que seu aplicativo é executado, clique em **Executar > executar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="24c14-238">Quando o aplicativo hello conclui a execução, você deve ver Olá saída no console do Eclipse Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="24c14-239">Faça logon no portal clássico do Azure de saudação e clique em **aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="24c14-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="24c14-240">novo aplicativo web e Olá deve aparecer na lista de aplicativos Web hello dentro de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="24c14-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="24c14-241">Implantando um aplicativo Web de toohello do aplicativo</span><span class="sxs-lookup"><span data-stu-id="24c14-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="24c14-242">Depois que você executou AzureWebDemo e criou um novo aplicativo de web hello, faça logon no portal clássico do hello, clique em **aplicativos Web**e selecione **WebDemoWebApp** em Olá **aplicativos Web** lista.</span><span class="sxs-lookup"><span data-stu-id="24c14-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="24c14-243">Na página do painel do aplicativo da web hello, clique em **procurar** (ou clique em URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="24c14-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="24c14-244">Você verá uma página de espaço reservado em branco, porque nenhum conteúdo foi publicado toohello web aplicativo ainda.</span><span class="sxs-lookup"><span data-stu-id="24c14-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="24c14-245">Em seguida você criará um aplicativo "Hello World" e implantá-lo toohello web app.</span><span class="sxs-lookup"><span data-stu-id="24c14-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="24c14-246">Criar um aplicativo Olá Mundo</span><span class="sxs-lookup"><span data-stu-id="24c14-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="24c14-247">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="24c14-247">Create hello application</span></span>
<span data-ttu-id="24c14-248">Em ordem toodemonstrate como toodeploy web de toohello um aplicativo, Olá procedimento a seguir mostra como toocreate um aplicativo "Hello World" Java simples e carregá-lo toohello aplicativo serviço Web de aplicativo que criou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="24c14-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="24c14-249">Clique em **Arquivo > Novo > Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="24c14-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="24c14-250">Nomeie-o `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="24c14-250">Name it `JSPHello`.</span></span> <span data-ttu-id="24c14-251">Não é necessário toochange outras configurações nesta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24c14-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="24c14-252">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="24c14-253">No Explorador de projeto, expanda Olá **JSPHello** de projeto, clique no **WebContent**, em seguida, clique em **Novo > arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="24c14-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="24c14-254">Na caixa de diálogo de novo arquivo JSP hello, nomeie o novo arquivo de saudação `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="24c14-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="24c14-255">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-255">Click **Next**.</span></span>
3. <span data-ttu-id="24c14-256">Em Olá **Selecionar modelo JSP** caixa de diálogo, selecione **novo arquivo JSP (html)** e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="24c14-257">No index.jsp, adicione Olá Olá código a seguir `<head>` e `<body>` marca seções:</span><span class="sxs-lookup"><span data-stu-id="24c14-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="24c14-258">Executar o aplicativo hello World Olá no localhost</span><span class="sxs-lookup"><span data-stu-id="24c14-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="24c14-259">Antes de executar este aplicativo, você precisa tooconfigure algumas propriedades.</span><span class="sxs-lookup"><span data-stu-id="24c14-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="24c14-260">Saudação de atalho **JSPHello** do projeto e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="24c14-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="24c14-261">Em hello **propriedades** caixa de diálogo: selecione **caminho de compilação de Java**, selecione Olá **ordenar e exportar** guia, verifique **JRE biblioteca do sistema**, em seguida, clique em **Backup** toomove-toohello superior da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="24c14-262">Também no hello **propriedades** caixa de diálogo: selecione **tempos de execução de destino** e clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="24c14-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="24c14-263">Em Olá **novo ambiente de tempo de execução do servidor** caixa de diálogo, selecione um servidor, como **versão 7.0 do Apache Tomcat** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="24c14-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="24c14-264">Em Olá **servidor Tomcat** caixa de diálogo, defina **nome** muito`Apache Tomcat v7.0`e defina **diretório de instalação do Tomcat** toohello diretório no qual você instalou a versão de saudação do Servidor Tomcat toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="24c14-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="24c14-265">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-265">Click **Finish**.</span></span>
5. <span data-ttu-id="24c14-266">Você, em seguida, retornar toohello **tempos de execução de destino** página de saudação **propriedades** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24c14-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="24c14-267">Selecione **Apache Tomcat v7.0** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="24c14-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="24c14-268">Em Olá Eclipse **executar** menu, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="24c14-269">Em Olá **executar como** caixa de diálogo, selecione **executado no servidor**.</span><span class="sxs-lookup"><span data-stu-id="24c14-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="24c14-270">Em Olá **executado no servidor** caixa de diálogo, selecione **Tomcat v 7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="24c14-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="24c14-271">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="24c14-271">Click **Finish**.</span></span>
7. <span data-ttu-id="24c14-272">Olá quando o aplicativo é executado, você deve ver Olá **JSPHello** página exibida em uma janela de localhost no Eclipse (`http://localhost:8080/JSPHello/`), exibindo Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="24c14-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="24c14-273">Exportar aplicativo hello como um WAR</span><span class="sxs-lookup"><span data-stu-id="24c14-273">Export hello application as a WAR</span></span>
<span data-ttu-id="24c14-274">Exporte arquivos de projeto web hello como um arquivo da web (WAR) para que você possa implantar aplicativo da web de toohello.</span><span class="sxs-lookup"><span data-stu-id="24c14-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="24c14-275">Olá seguintes arquivos de projeto web residem na pasta de conteúdo da Web hello:</span><span class="sxs-lookup"><span data-stu-id="24c14-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="24c14-276">Pasta de conteúdo da Web hello e selecione **exportar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="24c14-277">Em Olá **exportar selecione** caixa de diálogo, clique em **Web > WAR** arquivo e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="24c14-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="24c14-278">Em Olá **WAR exportar** caixa de diálogo, selecione diretório src de saudação no projeto atual Olá e incluir nome de Olá de arquivo WAR de saudação final hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="24c14-279">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="24c14-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="24c14-280">Para obter mais informações sobre como implantar arquivos WAR, consulte [adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="24c14-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="24c14-281">Implantando Olá Olá mundo de aplicativos usando o FTP</span><span class="sxs-lookup"><span data-stu-id="24c14-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="24c14-282">Selecione um aplicativo de terceiros FTP cliente toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="24c14-283">Este procedimento descreve duas opções: console de Kudu Olá embutido no Azure. e FileZilla, uma ferramenta popular com uma interface do usuário gráfica, conveniente.</span><span class="sxs-lookup"><span data-stu-id="24c14-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="24c14-284">**Observação:** Olá Kit de ferramentas do Azure para Eclipse dá suporte a contas de toostorage de implantação e a nuvem de serviços, mas não oferece suporte a aplicativos de tooweb de implantação.</span><span class="sxs-lookup"><span data-stu-id="24c14-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="24c14-285">Você pode implantar toostorage contas e serviços usando um projeto de implantação do Azure conforme descrito em nuvem [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), mas não tooweb aplicativos.</span><span class="sxs-lookup"><span data-stu-id="24c14-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="24c14-286">Use outros métodos como FTP ou GitHub tootransfer arquivos tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="24c14-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="24c14-287">**Observação:** não recomendamos o uso de FTP do prompt de comando do Windows hello (Olá de linha de comando FTP.EXE utilitário fornecido com o Windows).</span><span class="sxs-lookup"><span data-stu-id="24c14-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="24c14-288">Clientes FTP que usam o FTP ativo, como FTP.EXE, geralmente failover toowork firewalls.</span><span class="sxs-lookup"><span data-stu-id="24c14-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="24c14-289">FTP ativo Especifica um endereço interno da rede local, servidor toowhich um FTP provavelmente falharão tooconnect.</span><span class="sxs-lookup"><span data-stu-id="24c14-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="24c14-290">Para obter mais informações sobre o aplicativo de implantação tooan do serviço de aplicativo web usando FTP, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="24c14-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="24c14-291">Implantar usando um utilitário FTP</span><span class="sxs-lookup"><span data-stu-id="24c14-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="24c14-292">Configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="24c14-292">Set up deployment credentials</span></span>
<span data-ttu-id="24c14-293">Verifique se você executou Olá **AzureWebDemo** toocreate aplicativo um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="24c14-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="24c14-294">Você transferirá toothis local dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="24c14-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="24c14-295">Faça logon no portal clássico do hello e clique em **aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="24c14-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="24c14-296">Certifique-se de **WebDemoWebApp** aparece na lista de saudação de aplicativos web e certifique-se de que ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="24c14-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="24c14-297">Clique em **WebDemoWebApp** tooopen sua **painel** página.</span><span class="sxs-lookup"><span data-stu-id="24c14-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="24c14-298">Em Olá **painel** página em **rápidos**, clique em **configurar suas credenciais de implantação** (se você já tiver credenciais de implantação, lê  **Redefinir as credenciais de implantação**).</span><span class="sxs-lookup"><span data-stu-id="24c14-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="24c14-299">As credenciais de implantação estão associadas com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="24c14-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="24c14-300">Você precisa toospecify um nome de usuário e senha que você pode usar toodeploy usando Git e FTP.</span><span class="sxs-lookup"><span data-stu-id="24c14-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="24c14-301">Você pode usar essas credenciais toodeploy tooany web app em todas as assinaturas do Azure associadas à sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="24c14-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="24c14-302">Forneça credenciais de implantação do Git e FTP na caixa de diálogo Olá e saudação de registro de nome de usuário e senha para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="24c14-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="24c14-303">Obter informações de conexão de FTP</span><span class="sxs-lookup"><span data-stu-id="24c14-303">Get FTP connection information</span></span>
<span data-ttu-id="24c14-304">toouse FTP toodeploy aplicativo arquivos toohello recém-criado web aplicativo precisar de informações de conexão tooobtain.</span><span class="sxs-lookup"><span data-stu-id="24c14-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="24c14-305">Há duas maneiras de obter informações de conexão tooobtain.</span><span class="sxs-lookup"><span data-stu-id="24c14-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="24c14-306">É uma maneira toovisit Olá web aplicativo **painel** página; hello outra forma é toodownload Olá web aplicativo o perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="24c14-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="24c14-307">saudação de perfil de publicação é um arquivo XML que fornece informações como credenciais de logon e o nome de host do FTP para seus aplicativos web no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="24c14-308">Você pode usar o nome de usuário e senha toodeploy tooany aplicativo web em todas as assinaturas associadas à saudação conta do Azure, não apenas esse um.</span><span class="sxs-lookup"><span data-stu-id="24c14-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="24c14-309">informações de conexão tooobtain FTP na folha do aplicativo da web de saudação em Olá [Portal do Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="24c14-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="24c14-310">Em **Essentials**, localize e copie Olá **hostname de FTP**.</span><span class="sxs-lookup"><span data-stu-id="24c14-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="24c14-311">Este é um URI semelhante muito`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="24c14-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="24c14-312">Em **Essentials**, localize e copie o **nome de usuário de implantação/FTP**.</span><span class="sxs-lookup"><span data-stu-id="24c14-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="24c14-313">Isso terá o formato de saudação *webappname\deployment-username*; por exemplo `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="24c14-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="24c14-314">perfil de publicação de informações de conexão de FTP tooobtain da saudação:</span><span class="sxs-lookup"><span data-stu-id="24c14-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="24c14-315">Na folha do seu aplicativo da web hello, clique em **obter perfil de publicação**.</span><span class="sxs-lookup"><span data-stu-id="24c14-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="24c14-316">Isso baixará uma unidade de local de tooyour do arquivo. publishsettings.</span><span class="sxs-lookup"><span data-stu-id="24c14-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="24c14-317">Abra o arquivo. publishsettings de saudação em um editor de XML ou editor de texto e localize Olá `<publishProfile>` elemento que contém `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="24c14-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="24c14-318">Ele deve ter aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="24c14-319">Observe a esse aplicativo web de saudação `publishProfile` configurações mapeiam toohello FileZilla Site Manager configurações da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="24c14-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="24c14-320">`publishUrl`é Olá igual **nome de host do FTP**, Olá valor definido em **Host**.</span><span class="sxs-lookup"><span data-stu-id="24c14-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="24c14-321">`publishMethod="FTP"`significa que você definir **protocolo** muito**FTP - File Transfer Protocol**, e **criptografia** muito**usar FTP simples**.</span><span class="sxs-lookup"><span data-stu-id="24c14-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="24c14-322">`userName`e `userPWD` são chaves para Olá reais valores de nome de usuário e senha especificados quando você redefine credenciais de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="24c14-323">`userName`é Olá igual **implantação / FTP usuário**.</span><span class="sxs-lookup"><span data-stu-id="24c14-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="24c14-324">Eles mapeiam muito**usuário** e **senha** em FileZilla.</span><span class="sxs-lookup"><span data-stu-id="24c14-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="24c14-325">`ftpPassiveMode="True"`significa que esse site Olá FTP usa transferência por FTP passiva; Selecione **passivo** em Olá **as configurações de transferência** guia.</span><span class="sxs-lookup"><span data-stu-id="24c14-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="24c14-326">Configurar o aplicativo Web de saudação toohost um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="24c14-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="24c14-327">Antes de publicar o aplicativo hello, é necessário toochange algumas definições de configuração para que hello aplicativo web pode hospedar um aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="24c14-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="24c14-328">No portal clássico do hello, vá do aplicativo da web toohello **painel** página e clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="24c14-329">Em Olá **configurar** especifique Olá configurações a seguir.</span><span class="sxs-lookup"><span data-stu-id="24c14-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="24c14-330">Em **versão do Java** saudação padrão é **Off**; selecione versão do Java Olá destinos seu aplicativo; por exemplo 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="24c14-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="24c14-331">Depois de fazer isso, verifique também **contêiner da Web** é definir a versão de tooa do servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="24c14-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="24c14-332">Em **documentos padrão**, adicione JSP e movê-lo para cima toohello superior da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="24c14-333">(o arquivo de padrão de saudação para aplicativos web é hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="24c14-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="24c14-334">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="24c14-335">Publicar seu aplicativo usando Kudu</span><span class="sxs-lookup"><span data-stu-id="24c14-335">Publish your application using Kudu</span></span>
<span data-ttu-id="24c14-336">Aplicativo de hello toopublish unidirecional é Olá toouse que kudu depurar console incorporada do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c14-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="24c14-337">O kudu é conhecido toobe estável e consistente com o serviço de aplicativo Web de aplicativos e servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="24c14-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="24c14-338">Você acessar o console de saudação do aplicativo web de saudação navegando tooa URL de saudação formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="24c14-339">Para esse procedimento, o console de Kudu de saudação está localizado em Olá seguindo a URL; Procure toothis local:</span><span class="sxs-lookup"><span data-stu-id="24c14-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="24c14-340">No menu superior do hello, selecione **Console depuração > CMD**.</span><span class="sxs-lookup"><span data-stu-id="24c14-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="24c14-341">Na linha de comando do console hello, navegue muito`/site/wwwroot` (ou clique em `site`, em seguida, `wwwroot` no modo de exibição de diretório de saudação na parte superior de saudação da página de saudação):</span><span class="sxs-lookup"><span data-stu-id="24c14-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="24c14-342">Depois de especificar a **Versão do Java**, o servidor Tomcat deve criar uma pasta webapps.</span><span class="sxs-lookup"><span data-stu-id="24c14-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="24c14-343">Na linha de comando do console hello, navegar toohello webapps diretório:</span><span class="sxs-lookup"><span data-stu-id="24c14-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="24c14-344">Arraste JSPHello.war de `<project-path>/JSPHello/src/` e inseri-la em modo de exibição de diretório Kudu de saudação em `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="24c14-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="24c14-345">Não arraste-a área "Arraste aqui tooupload e zip" toohello, porque o Tomcat será descompacte-o.</span><span class="sxs-lookup"><span data-stu-id="24c14-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="24c14-346">No primeiro JSPHello.war aparece na área de diretório de saudação por si só:</span><span class="sxs-lookup"><span data-stu-id="24c14-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="24c14-347">Em um curto período de tempo (provavelmente menos de 5 minutos) servidor Tomcat serão descompactados arquivo WAR de saudação em um diretório JSPHello descompactado.</span><span class="sxs-lookup"><span data-stu-id="24c14-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="24c14-348">Clique em toosee de diretório raiz Olá se JSP foi descompactado e copiados para esse local.</span><span class="sxs-lookup"><span data-stu-id="24c14-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="24c14-349">Nesse caso, navegue toohello back webapps diretório toosee se Olá desempacotados JSPHello diretório foi criado.</span><span class="sxs-lookup"><span data-stu-id="24c14-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="24c14-350">Se você não ver esses itens, aguarde e repita.</span><span class="sxs-lookup"><span data-stu-id="24c14-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="24c14-351">Publicar seu aplicativo usando o FileZilla (opcional)</span><span class="sxs-lookup"><span data-stu-id="24c14-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="24c14-352">Outra ferramenta que você pode usar o aplicativo de hello toopublish é FileZilla, um cliente FTP de terceiros popular com uma interface do usuário gráfica, conveniente.</span><span class="sxs-lookup"><span data-stu-id="24c14-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="24c14-353">Você pode baixar e instalar o FileZilla de [http://filezilla-project.org/](http://filezilla-project.org/) se você ainda não o tiver.</span><span class="sxs-lookup"><span data-stu-id="24c14-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="24c14-354">Para obter mais informações sobre como usar o cliente hello, consulte Olá [FileZilla documentação](https://wiki.filezilla-project.org/Documentation) e essa entrada de blog em [os clientes FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="24c14-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="24c14-355">No FileZilla, clique em **Arquivo > Gerenciador de Sites**.</span><span class="sxs-lookup"><span data-stu-id="24c14-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="24c14-356">Em Olá **Site Manager** caixa de diálogo, clique em **novo Site**.</span><span class="sxs-lookup"><span data-stu-id="24c14-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="24c14-357">Um novo site FTP em branco aparecerá no **Selecionar entrada** solicitando que você tooprovide um nome.</span><span class="sxs-lookup"><span data-stu-id="24c14-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="24c14-358">Para este procedimento, nomeie-o como `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="24c14-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="24c14-359">Em Olá **geral** especifique Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="24c14-360">**Host:** Enter Olá **nome de Host do FTP** que você copiou do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="24c14-361">**Porta:** (deixe em branco, pois isso é uma transferência de passivo e servidor de saudação determinará Olá porta toouse.)</span><span class="sxs-lookup"><span data-stu-id="24c14-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="24c14-362">**Protocolo:** protocolo FTP</span><span class="sxs-lookup"><span data-stu-id="24c14-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="24c14-363">**Criptografia:** usar FTP simples</span><span class="sxs-lookup"><span data-stu-id="24c14-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="24c14-364">**Tipo de Logon:** normal</span><span class="sxs-lookup"><span data-stu-id="24c14-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="24c14-365">**Usuário:** Enter Olá implantação / FTP de usuário que você copiou do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="24c14-366">Isso é Olá completo FTP nome de usuário, que tem o formato de saudação *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="24c14-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="24c14-367">**Senha:** digite a senha Olá especificado quando você define as credenciais de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="24c14-368">Em Olá **as configurações de transferência** guia, selecione **passivo**.</span><span class="sxs-lookup"><span data-stu-id="24c14-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="24c14-369">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-369">Click **Connect**.</span></span> <span data-ttu-id="24c14-370">Se for bem-sucedida, console da FileZilla exibirá um `Status: Connected` mensagem e emitir um `LIST` conteúdo do diretório Olá toolist de comando.</span><span class="sxs-lookup"><span data-stu-id="24c14-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="24c14-371">Em Olá **Local** reside do painel do site, diretório de origem Olá select no arquivo hello JSPHello.war; caminho Olá será a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="24c14-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="24c14-372">Em Olá **remoto** painel do site, a pasta de destino de saudação select.</span><span class="sxs-lookup"><span data-stu-id="24c14-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="24c14-373">Você implantará Olá WAR arquivo toohello `webapps` diretório na raiz do aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="24c14-374">Navegue muito`/site/wwwroot`, clique duas vezes em `wwwroot`e selecione **criar diretório**.</span><span class="sxs-lookup"><span data-stu-id="24c14-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="24c14-375">Diretório de nome de saudação `webapps` e insira o diretório.</span><span class="sxs-lookup"><span data-stu-id="24c14-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="24c14-376">Transferir JSPHello.war muito`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="24c14-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="24c14-377">Selecione JSPHello.war no hello **Local** lista de arquivos, clique com botão direito nele e selecione **carregar**.</span><span class="sxs-lookup"><span data-stu-id="24c14-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="24c14-378">Você deverá vê-lo aparecer em `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="24c14-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="24c14-379">Depois de copiar o diretório de webapps toohello JSPHello.war, servidor Tomcat será automaticamente Descompacte (unzip) Olá arquivos contidos no arquivo WAR hello.</span><span class="sxs-lookup"><span data-stu-id="24c14-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="24c14-380">Embora o servidor Tomcat começa desempacotar quase imediatamente, pode levar um longo tempo (possivelmente horas) para Olá arquivos tooappear no cliente FTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="24c14-381">Executar o aplicativo hello World Olá em Olá Web App</span><span class="sxs-lookup"><span data-stu-id="24c14-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="24c14-382">Após Olá WAR arquivo carregado e verificado que o servidor Tomcat criou um desempacotados `JSPHello` diretório, procurar muito`http://webdemowebapp.azurewebsites.net/JSPHello` aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="24c14-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="24c14-383">**Observação:** se você clicar em **procurar** no portal clássico do hello, você pode obter, página da Web padrão do hello dizendo "Este aplicativo web de Java com base tem foi criado com êxito."</span><span class="sxs-lookup"><span data-stu-id="24c14-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="24c14-384">Você pode ter toorefresh Olá página na saída do aplicativo hello ordem tooview em vez de página da Web padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="24c14-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="24c14-385">Quando o aplicativo hello é executado, você verá uma página da web com hello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="24c14-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="24c14-386">Limpar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="24c14-386">Clean up Azure resources</span></span>
<span data-ttu-id="24c14-387">Este procedimento cria um aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="24c14-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="24c14-388">Você será cobrado para o recurso de saudação desde que ele existe.</span><span class="sxs-lookup"><span data-stu-id="24c14-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="24c14-389">A menos que você planeje toocontinue usando Olá web app para teste ou desenvolvimento, você deve considerar parando ou excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="24c14-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="24c14-390">Um aplicativo Web cuja execução foi interrompida ainda incorrerá em um pequeno encargo, mas você poderá reiniciá-lo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="24c14-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="24c14-391">Excluir um aplicativo web apaga todos os dados que você carregou tooit.</span><span class="sxs-lookup"><span data-stu-id="24c14-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

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
