---
title: aaaManage certificados em um cluster do Azure Service Fabric | Microsoft Docs
description: "Descreve como tooadd novos certificados, o certificado de substituição e remover certificados tooor de um cluster do Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="c3c04-103">Adicionar ou remover certificados para um cluster do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="c3c04-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="c3c04-104">É recomendável que você se familiarize com como o serviço de malha usa certificados x. 509 e estar familiarizado com hello [cenários de segurança de Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="c3c04-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="c3c04-105">Você deve entender o que é um certificado de cluster e qual sua finalidade, antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c3c04-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="c3c04-106">Segurança do certificado de serviço permite a malha que você especificar que dois cluster certificados, um principal e um secundário, quando você configurar durante a criação do cluster, em certificados de tooclient de adição.</span><span class="sxs-lookup"><span data-stu-id="c3c04-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="c3c04-107">Consulte também[criando um cluster do azure por meio do portal](service-fabric-cluster-creation-via-portal.md) ou [criando um cluster do azure por meio do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obter detalhes sobre a configuração no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="c3c04-108">Se você especificar apenas um certificado de cluster no momento da criação, que será usado como certificado principal hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="c3c04-109">Após a criação do cluster, é possível adicionar um novo certificado como um secundário.</span><span class="sxs-lookup"><span data-stu-id="c3c04-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="c3c04-110">Para um cluster seguro, sempre precisará de pelo menos um cluster (não revogado e não expirado) válido certificado (primário ou secundário) implantado (se não, Olá cluster parará de funcionar).</span><span class="sxs-lookup"><span data-stu-id="c3c04-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="c3c04-111">90 dias antes de todos os certificados válidos alcançar expiração, sistema hello gera um rastreamento de avisos e também um evento de integridade de aviso no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="c3c04-112">Atualmente, não há nenhum email nem qualquer outra notificação enviada pelo Service Fabric sobre esse tópico.</span><span class="sxs-lookup"><span data-stu-id="c3c04-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="c3c04-113">Adicionar um certificado de cluster secundário usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="c3c04-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="c3c04-114">Certificado de cluster secundário não pode ser adicionado por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3c04-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="c3c04-115">Você tem toouse Azure powershell para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c3c04-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="c3c04-116">Olá processo é descrito neste documento.</span><span class="sxs-lookup"><span data-stu-id="c3c04-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="c3c04-117">Trocar Olá certificados de cluster usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="c3c04-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="c3c04-118">Depois de ter implantado com êxito um certificado de cluster secundário, se você quiser tooswap Olá primários e secundários, em seguida, navegue toohello folha de segurança e selecione a opção de 'Troca com primário' de saudação da saudação contexto menu tooswap Olá secundário cert com cert primário da saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Trocar o certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="c3c04-120">Remover um certificado de cluster usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="c3c04-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="c3c04-121">Para um cluster seguro, sempre será necessário pelo menos um (não revogado e não expirado) certificado válido (primário ou secundário) implantado se não, Olá cluster parará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="c3c04-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="c3c04-122">tooremove certificado secundário seja usado para segurança de cluster, folha de segurança toohello navegue e selecione Olá 'Delete' opção no menu de contexto de saudação no certificado secundário hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="c3c04-123">Se sua intenção for certificado Olá tooremove está marcado como primário, em seguida, você precisará tooswap com hello secundário primeiro e exclua Olá secundário após a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="c3c04-124">Adicionar um certificado secundário usando o Powershell do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c3c04-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="c3c04-125">Essas etapas pressupõem que estão familiarizados com o funcionamento do Gerenciador de recursos de ter implantado pelo menos um cluster de malha do serviço usando um modelo do Gerenciador de recursos e ter Olá modelo que você usou tooset útil do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="c3c04-126">Presume-se também que você esteja familiarizado com o uso do JSON.</span><span class="sxs-lookup"><span data-stu-id="c3c04-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="c3c04-127">Se você estiver procurando um modelo de exemplo e parâmetros que você pode usar toofollow ao longo ou como um ponto de partida, baixá-lo neste [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="c3c04-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="c3c04-128">Editar o modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c3c04-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="c3c04-129">Para facilitar a seguir ao longo, o exemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contém todas as edições de saudação que realizaremos.</span><span class="sxs-lookup"><span data-stu-id="c3c04-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="c3c04-130">exemplo Hello está disponível em [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="c3c04-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="c3c04-131">**Verifique se toofollow todas as etapas de saudação**</span><span class="sxs-lookup"><span data-stu-id="c3c04-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="c3c04-132">**Etapa 1:** abra o modelo do Gerenciador de recursos de saudação usada toodeploy Cluster.</span><span class="sxs-lookup"><span data-stu-id="c3c04-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="c3c04-133">(Se você baixou o exemplo hello Olá acima repositório, usar 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy um cluster seguro e, em seguida, abra o modelo).</span><span class="sxs-lookup"><span data-stu-id="c3c04-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="c3c04-134">**Etapa 2:** adicionar **dois novos parâmetros** "secCertificateThumbprint" e "secCertificateUrlValue" do tipo "cadeia de caracteres" toohello seção de parâmetro do modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="c3c04-135">Você pode copiar Olá trecho de código a seguir e adicione-o modelo toohello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="c3c04-136">Dependendo da fonte de saudação do seu modelo, você pode já ter definido, caso mover toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="c3c04-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="c3c04-137">**Etapa 3:** fazer alterações toohello **Microsoft.ServiceFabric/clusters** recurso - Localizar a definição de recurso "Microsoft.ServiceFabric/clusters" hello em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="c3c04-138">Propriedades dessa definição, você encontrará "Certificate" JSON marca, que deve ser algo como Olá trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3c04-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="c3c04-139">Adicione uma nova marcação “thumbprintSecondary” e atribua a ela um valor de “[parameters('secCertificateThumbprint')]”.</span><span class="sxs-lookup"><span data-stu-id="c3c04-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="c3c04-140">Agora, a definição de recurso Olá deve ser semelhante Olá seguinte (dependendo de sua fonte de modelo hello, pode não ser exatamente como Olá trecho abaixo).</span><span class="sxs-lookup"><span data-stu-id="c3c04-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="c3c04-141">Se você quiser muito**cert de saudação de substituição**, em seguida, especifique o novo certificado de saudação como primária atual do primário e movendo hello como secundário.</span><span class="sxs-lookup"><span data-stu-id="c3c04-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="c3c04-142">Isso resulta na substituição de saudação do seu certificado de novo de toohello atual do certificado primário em uma etapa de implantação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="c3c04-143">**Etapa 4:** fazer alterações muito**todos os** Olá **Microsoft.Compute/virtualMachineScaleSets** definições de recursos - Localizar Olá Microsoft.Compute/virtualMachineScaleSets recurso definição.</span><span class="sxs-lookup"><span data-stu-id="c3c04-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="c3c04-144">Role toohello "publisher": "Microsoft.Azure.ServiceFabric", em "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="c3c04-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="c3c04-145">Configurações do publicador da malha Olá serviço, você verá algo assim.</span><span class="sxs-lookup"><span data-stu-id="c3c04-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="c3c04-147">Adicionar Olá novo certificado entradas tooit</span><span class="sxs-lookup"><span data-stu-id="c3c04-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="c3c04-148">Propriedades de saudação agora devem se parecer com</span><span class="sxs-lookup"><span data-stu-id="c3c04-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="c3c04-150">Se você quiser muito**cert de saudação de substituição**, em seguida, especifique o novo certificado de saudação como primária atual do primário e movendo hello como secundário.</span><span class="sxs-lookup"><span data-stu-id="c3c04-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="c3c04-151">Isso resulta na substituição de saudação do seu certificado de novo de toohello atual do certificado em uma etapa de implantação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="c3c04-152">Propriedades de saudação agora devem se parecer com</span><span class="sxs-lookup"><span data-stu-id="c3c04-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="c3c04-154">**Etapa 5:** fazer alterações muito**todos os** Olá **Microsoft.Compute/virtualMachineScaleSets** definições de recursos - Localizar Olá Microsoft.Compute/virtualMachineScaleSets recurso definição.</span><span class="sxs-lookup"><span data-stu-id="c3c04-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="c3c04-155">Role toohello "vaultCertificates":, em "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="c3c04-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="c3c04-156">O resultado deve ser semelhante a este.</span><span class="sxs-lookup"><span data-stu-id="c3c04-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="c3c04-158">Adicione Olá secCertificateUrlValue tooit.</span><span class="sxs-lookup"><span data-stu-id="c3c04-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="c3c04-159">Use Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3c04-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="c3c04-160">Agora Olá resultante Json deve ser semelhante isso.</span><span class="sxs-lookup"><span data-stu-id="c3c04-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="c3c04-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="c3c04-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="c3c04-162">Certifique-se de que tem repetido as etapas 4 e 5 para todas as definições de recursos de Nodetypes/Microsoft.Compute/virtualMachineScaleSets Olá no modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="c3c04-163">Se você perder um deles, certificado Olá não será instalado em que VMSS e você terá resultados imprevisíveis em seu cluster, incluindo cluster Olá ficar inativo (se você acabará com nenhum certificado válido que nesse cluster Olá pode usar para segurança.</span><span class="sxs-lookup"><span data-stu-id="c3c04-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="c3c04-164">Portanto, verifique, antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c3c04-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="c3c04-165">Editar seu modelo arquivo tooreflect Olá novos parâmetros adicionados acima</span><span class="sxs-lookup"><span data-stu-id="c3c04-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="c3c04-166">Se você estiver usando o exemplo hello da saudação [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow, você pode iniciar toomake alterações no hello exemplo 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="c3c04-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="c3c04-167">Editar seu arquivo de parâmetro de modelo do Gerenciador de recursos, adicione Olá dois novos parâmetros para secCertificateThumbprint e secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="c3c04-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="c3c04-168">Implantar Olá modelo tooAzure</span><span class="sxs-lookup"><span data-stu-id="c3c04-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="c3c04-169">Você está agora pronto toodeploy tooAzure seu modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="c3c04-170">Abra um prompt de comando do Azure PS versão 1+.</span><span class="sxs-lookup"><span data-stu-id="c3c04-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="c3c04-171">Faça logon no tooyour conta do Azure e selecione a assinatura do azure específico do hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="c3c04-172">Essa é uma etapa importante para quem tem acesso toomore que uma assinatura do azure.</span><span class="sxs-lookup"><span data-stu-id="c3c04-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="c3c04-173">Testar Olá modelo anterior toodeploying-lo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="c3c04-174">Use Olá mesmo grupo de recursos que o cluster está implantado atualmente.</span><span class="sxs-lookup"><span data-stu-id="c3c04-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="c3c04-175">Implante grupo de recursos de tooyour Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="c3c04-176">Use Olá mesmo grupo de recursos que o cluster está implantado atualmente.</span><span class="sxs-lookup"><span data-stu-id="c3c04-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="c3c04-177">Execute Olá AzureRmResourceGroupDeployment novo comando.</span><span class="sxs-lookup"><span data-stu-id="c3c04-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="c3c04-178">Modo de saudação toospecify, não é necessário desde que o valor padrão de saudação é **incremental**.</span><span class="sxs-lookup"><span data-stu-id="c3c04-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="c3c04-179">Se você definir o modo tooComplete, você pode excluir por engano recursos que não estão no modelo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="c3c04-180">Portanto, não o use neste cenário.</span><span class="sxs-lookup"><span data-stu-id="c3c04-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="c3c04-181">Aqui está um preenchido saída de exemplo de hello mesmo powershell.</span><span class="sxs-lookup"><span data-stu-id="c3c04-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="c3c04-182">Após a conclusão da implantação Olá, conecte-se usando o cluster tooyour Olá novo certificado e executar algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="c3c04-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="c3c04-183">Se você é capaz de toodo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-183">If you are able toodo.</span></span> <span data-ttu-id="c3c04-184">Em seguida, você pode excluir o certificado antigo hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="c3c04-185">Se você estiver usando um certificado autoassinado, não se esqueça de tooimport-los no repositório de certificados local TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="c3c04-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="c3c04-186">Para referência rápida aqui é cluster seguro do hello comando tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="c3c04-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="c3c04-187">Para referência rápida aqui está a integridade do cluster tooget Olá comando</span><span class="sxs-lookup"><span data-stu-id="c3c04-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="c3c04-188">Implantação de cluster de toohello de certificados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3c04-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="c3c04-189">Você pode usar o hello mesmo etapas, conforme descrito nas etapas 5 acima toohave Olá certificados implantados por meio de um toohello keyvault nós.</span><span class="sxs-lookup"><span data-stu-id="c3c04-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="c3c04-190">apenas é necessário definir e usar parâmetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="c3c04-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="c3c04-191">Adicionando ou removendo certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="c3c04-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="c3c04-192">No certificado de cluster toohello adição, você pode adicionar operações de gerenciamento de tooperform de certificados de cliente em um cluster do service fabric.</span><span class="sxs-lookup"><span data-stu-id="c3c04-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="c3c04-193">Você pode adicionar dois tipos de certificados de cliente - Admin ou Somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c3c04-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="c3c04-194">Em seguida, podem ser usados toocontrol operações de administração de toohello de acesso e operações de consulta no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="c3c04-195">Por padrão, os certificados de cluster de saudação são adicionados toohello administrador certificados lista de permissões.</span><span class="sxs-lookup"><span data-stu-id="c3c04-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="c3c04-196">Você pode especificar qualquer número de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="c3c04-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="c3c04-197">Cada adição ou exclusão resulta em um cluster do configuração update toohello service fabric</span><span class="sxs-lookup"><span data-stu-id="c3c04-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="c3c04-198">A adição de certificados de cliente - Admin ou somente leitura por meio do portal</span><span class="sxs-lookup"><span data-stu-id="c3c04-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="c3c04-199">Navegue toohello folha de segurança e selecione Olá '+ autenticação' botão na parte superior da folha de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="c3c04-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="c3c04-200">Na folha de 'Adicionar autenticação' hello, escolha Olá 'Tipo de autenticação' - 'Cliente somente leitura' ou 'client Admin'</span><span class="sxs-lookup"><span data-stu-id="c3c04-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="c3c04-201">Escolha método de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="c3c04-202">Isso indica tooService Fabric se ele deve pesquisar o certificado usando o nome da entidade hello ou impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3c04-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="c3c04-203">Em geral, não é um método de autorização segurança boa prática toouse Olá do nome da entidade.</span><span class="sxs-lookup"><span data-stu-id="c3c04-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Adicionar certificado de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="c3c04-205">Exclusão de certificados de cliente - Admin ou somente leitura usando Olá portal</span><span class="sxs-lookup"><span data-stu-id="c3c04-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="c3c04-206">tooremove certificado secundário seja usado para segurança de cluster, folha de segurança toohello navegue e selecione Olá 'Delete' opção no menu de contexto de saudação no certificado específico Olá.</span><span class="sxs-lookup"><span data-stu-id="c3c04-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c3c04-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3c04-207">Next steps</span></span>
<span data-ttu-id="c3c04-208">Leia estes artigos para obter mais informações sobre gerenciamento de cluster:</span><span class="sxs-lookup"><span data-stu-id="c3c04-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="c3c04-209">Processo de atualização de Cluster de Malha do Serviço e as suas expectativas</span><span class="sxs-lookup"><span data-stu-id="c3c04-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="c3c04-210">Configurar o acesso baseado em funções para clientes</span><span class="sxs-lookup"><span data-stu-id="c3c04-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


