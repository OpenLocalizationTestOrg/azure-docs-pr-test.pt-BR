---
title: "Configurar conexões seguras do cluster do Service Fabric | Microsoft Docs"
description: "Saiba mais sobre como usar o Visual Studio para configurar conexões seguras às quais o cluster do Azure Service Fabric dá suporte."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: dc07b2f38d6fd2de941ebbe99303f6e63cbf122d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-connections-to-a-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="3440d-103">Configurar conexões seguras para um cluster do Service Fabric do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3440d-103">Configure secure connections to a Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="3440d-104">Saiba mais sobre como usar o Visual Studio para acessar com segurança um cluster do Service Fabric do Azure com políticas de controle de acesso configuradas.</span><span class="sxs-lookup"><span data-stu-id="3440d-104">Learn how to use Visual Studio to securely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="3440d-105">Tipos de conexão do cluster</span><span class="sxs-lookup"><span data-stu-id="3440d-105">Cluster connection types</span></span>
<span data-ttu-id="3440d-106">O cluster do Azure Service Fabric dá suporte a dois tipos de conexão: conexões **não seguras** e conexões seguras **baseadas no certificado x509**.</span><span class="sxs-lookup"><span data-stu-id="3440d-106">Two types of connections are supported by the Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="3440d-107">(Para clusters do Service Fabric hospedados localmente, também há suporte para autenticações do **Windows** e **dSTS**.) Você precisa configurar o tipo de conexão de cluster durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="3440d-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have to configure the cluster connection type when the cluster is being created.</span></span> <span data-ttu-id="3440d-108">Depois de criado, o tipo de conexão não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="3440d-108">Once it's created, the connection type can’t be changed.</span></span>

<span data-ttu-id="3440d-109">As Ferramentas do Service Fabric do Visual Studio dão suporte a todos os tipos de autenticação para conexão com um cluster para publicação.</span><span class="sxs-lookup"><span data-stu-id="3440d-109">The Visual Studio Service Fabric tools support all authentication types for connecting to a cluster for publishing.</span></span> <span data-ttu-id="3440d-110">Veja [Configurando um cluster do Service Fabric no Portal do Azure](service-fabric-cluster-creation-via-portal.md) para obter instruções sobre como configurar um cluster do Service Fabric seguro.</span><span class="sxs-lookup"><span data-stu-id="3440d-110">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how to set up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="3440d-111">Configurar conexões do cluster em perfis de publicação</span><span class="sxs-lookup"><span data-stu-id="3440d-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="3440d-112">Se você publicar um projeto do Service Fabric do Visual Studio, use a caixa de diálogo **Publicar Aplicativo do Service Fabric** para escolher um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3440d-112">If you publish a Service Fabric project from Visual Studio, use the **Publish Service Fabric Application** dialog box to choose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="3440d-113">Em **Ponto de extremidade de conexão**, selecione um cluster existente em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3440d-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![A caixa de diálogo **Publicar Aplicativo do Service Fabric** é usada para configurar uma conexão do Service Fabric.][publishdialog]

<span data-ttu-id="3440d-115">A caixa de diálogo **Publicar Aplicativo do Service Fabric** valida automaticamente a conexão do cluster.</span><span class="sxs-lookup"><span data-stu-id="3440d-115">The **Publish Service Fabric Application** dialog box automatically validates the cluster connection.</span></span> <span data-ttu-id="3440d-116">Se solicitado, entre em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3440d-116">If prompted, sign in to your Azure account.</span></span> <span data-ttu-id="3440d-117">Se a validação for bem-sucedida, significa que seu sistema possui os certificados corretos instalados para se conectar ao cluster com segurança, ou o cluster é não seguro.</span><span class="sxs-lookup"><span data-stu-id="3440d-117">If validation passes, it means that your system has the correct certificates installed to connect to the cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="3440d-118">As falhas de validação podem ser causadas por problemas de rede ou caso o sistema não tenha sido corretamente configurado para conectar-se a um cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="3440d-118">Validation failures can be caused by network issues or by not having your system correctly configured to connect to a secure cluster.</span></span>

![A caixa de diálogo **Publicar Aplicativo do Service Fabric** valida uma conexão de cluster do Service Fabric existente e corretamente configurada.][selectsfcluster]

### <a name="to-connect-to-a-secure-cluster"></a><span data-ttu-id="3440d-120">Para conectar-se a um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="3440d-120">To connect to a secure cluster</span></span>
1. <span data-ttu-id="3440d-121">Verifique se você pode acessar um dos certificados de cliente nos quais o cluster de destino confia.</span><span class="sxs-lookup"><span data-stu-id="3440d-121">Make sure you can access one of the client certificates that the destination cluster trusts.</span></span> <span data-ttu-id="3440d-122">Normalmente, o certificado é compartilhado como um arquivo de Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="3440d-122">The certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="3440d-123">Veja [Configurando um cluster do Service Fabric do Portal do Azure](service-fabric-cluster-creation-via-portal.md) para saber como configurar o servidor para conceder acesso a um cliente.</span><span class="sxs-lookup"><span data-stu-id="3440d-123">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for how to configure the server to grant access to a client.</span></span>
2. <span data-ttu-id="3440d-124">Instale o certificado confiável.</span><span class="sxs-lookup"><span data-stu-id="3440d-124">Install the trusted certificate.</span></span> <span data-ttu-id="3440d-125">Para fazer isso, clique duas vezes no arquivo .pfx ou use o script do PowerShell, Import-PfxCertificate, para importar os certificados.</span><span class="sxs-lookup"><span data-stu-id="3440d-125">To do this, double-click the .pfx file, or use the PowerShell script Import-PfxCertificate to import the certificates.</span></span> <span data-ttu-id="3440d-126">Instale o certificado em **Cert:\LocalMachine\My**.</span><span class="sxs-lookup"><span data-stu-id="3440d-126">Install the certificate to **Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="3440d-127">É possível aceitar todas as configurações padrão durante a importação do certificado.</span><span class="sxs-lookup"><span data-stu-id="3440d-127">It's OK to accept all default settings while importing the certificate.</span></span>
3. <span data-ttu-id="3440d-128">Escolha o comando **Publicar...** no menu de atalho do projeto para abrir a caixa de diálogo **Publicar Aplicativo do Azure** e selecione o cluster de destino.</span><span class="sxs-lookup"><span data-stu-id="3440d-128">Choose the **Publish...** command on the shortcut menu of the project to open the **Publish Azure Application** dialog box and then select the target cluster.</span></span> <span data-ttu-id="3440d-129">A ferramenta resolve automaticamente a conexão e salva os parâmetros da conexão segura no perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="3440d-129">The tool automatically resolves the connection and saves the secure connection parameters in the publish profile.</span></span>
4. <span data-ttu-id="3440d-130">Opcional: edite o perfil de publicação para especificar uma conexão segura de cluster.</span><span class="sxs-lookup"><span data-stu-id="3440d-130">Optional: You can edit the publish profile to specify a secure cluster connection.</span></span>
   
   <span data-ttu-id="3440d-131">Como você está editando manualmente o arquivo XML do Perfil de Publicação a fim de especificar as informações do certificado, anote o nome do repositório de certificados, do local de armazenamento e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="3440d-131">Since you're manually editing the Publish Profile XML file to specify the certificate information, be sure to note the certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="3440d-132">Você precisará fornecer esses valores para o nome e o local do repositório do certificado.</span><span class="sxs-lookup"><span data-stu-id="3440d-132">You'll need to provide these values for the certificate's store name and store location.</span></span> <span data-ttu-id="3440d-133">Confira [Como recuperar a impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="3440d-133">See [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="3440d-134">Você pode usar os parâmetros *ClusterConnectionParameters* para especificar os parâmetros do PowerShell a serem usados na conexão ao cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3440d-134">You can use the *ClusterConnectionParameters* parameters to specify the PowerShell parameters to use when connecting to the Service Fabric cluster.</span></span> <span data-ttu-id="3440d-135">Os parâmetros válidos são aqueles aceitos pelo cmdlet Connect-ServiceFabricCluster.</span><span class="sxs-lookup"><span data-stu-id="3440d-135">Valid parameters are any that are accepted by the Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="3440d-136">Confira [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) para obter uma lista dos parâmetros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3440d-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="3440d-137">Se você estiver publicando em um cluster remoto, será necessário especificar os parâmetros adequados para o cluster específico.</span><span class="sxs-lookup"><span data-stu-id="3440d-137">If you’re publishing to a remote cluster, you need to specify the appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="3440d-138">A seguir, um exemplo de conexão a um cluster não seguro:</span><span class="sxs-lookup"><span data-stu-id="3440d-138">The following is an example of connecting to a non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="3440d-139">Este é um exemplo para se conectar a um cluster seguro baseado em certificado X509:</span><span class="sxs-lookup"><span data-stu-id="3440d-139">Here’s an example for connecting to an x509 certificate-based secure cluster:</span></span>
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. <span data-ttu-id="3440d-140">Edite outras configurações necessárias, como os parâmetros de atualização e o local do arquivo de Parâmetro do Aplicativo e, em seguida, publique seu aplicativo na caixa de diálogo **Publicar Aplicativo do Service Fabric** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3440d-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from the **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3440d-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3440d-141">Next steps</span></span>
<span data-ttu-id="3440d-142">Para saber mais sobre como acessar os clusters do Service Fabric, confira [Visualizando o cluster usando o Explorador do Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3440d-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
