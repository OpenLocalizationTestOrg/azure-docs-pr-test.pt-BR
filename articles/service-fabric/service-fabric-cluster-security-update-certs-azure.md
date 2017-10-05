---
title: Gerenciar certificados em um cluster do Azure Service Fabric | Microsoft Docs
description: Descreve como adicionar novos certificados, sobrepor certificados e remover certificados de e para um cluster do Service Fabric.
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
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="2d32f-103">Adicionar ou remover certificados para um cluster do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="2d32f-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="2d32f-104">É recomendável que você se familiarize com o modo como o Service Fabric usa certificados X.509 e com os [Cenários de segurança do cluster do cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="2d32f-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="2d32f-105">Você deve entender o que é um certificado de cluster e qual sua finalidade, antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2d32f-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="2d32f-106">O Service Fabric permite especificar dois certificados de cluster, um primário e um secundário, quando você configura a segurança do certificado durante a criação do cluster, além de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="2d32f-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="2d32f-107">Veja a [criação de um cluster do Service Fabric por meio do portal](service-fabric-cluster-creation-via-portal.md) ou a [criação de um cluster do azure por meio do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obter detalhes sobre a configuração deles no tempo de criação.</span><span class="sxs-lookup"><span data-stu-id="2d32f-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="2d32f-108">Se você especificar apenas um certificado de cluster no momento da criação, em seguida, que é usado como o certificado principal.</span><span class="sxs-lookup"><span data-stu-id="2d32f-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="2d32f-109">Após a criação do cluster, é possível adicionar um novo certificado como um secundário.</span><span class="sxs-lookup"><span data-stu-id="2d32f-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="2d32f-110">Para um cluster seguro, você sempre precisará de, pelo menos, um certificado de cluster (primário ou secundário) válido (não revogado ou expirado) implantado; caso contrário, o cluster vai parar de funcionar.</span><span class="sxs-lookup"><span data-stu-id="2d32f-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="2d32f-111">Em 90 dias antes que todos os certificados válidos alcancem a expiração, o sistema gera um rastreamento de avisos e também um evento de integridade de aviso no nó.</span><span class="sxs-lookup"><span data-stu-id="2d32f-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="2d32f-112">Atualmente, não há nenhum email nem qualquer outra notificação enviada pelo Service Fabric sobre esse tópico.</span><span class="sxs-lookup"><span data-stu-id="2d32f-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="2d32f-113">Adicionar um certificado de cluster secundário usando o portal</span><span class="sxs-lookup"><span data-stu-id="2d32f-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="2d32f-114">Certificado de cluster secundário não pode ser adicionado por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d32f-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="2d32f-115">Você precisa usar o Azure powershell para isso.</span><span class="sxs-lookup"><span data-stu-id="2d32f-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="2d32f-116">O processo será descrito posteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="2d32f-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="2d32f-117">Trocar os certificados de cluster usando o portal</span><span class="sxs-lookup"><span data-stu-id="2d32f-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="2d32f-118">Depois de ter implantado com êxito um certificado de cluster secundário, se você deseja alternar primário e secundário, navegue até a folha de segurança e selecione a opção 'Troca com primário' no menu de contexto para trocar o certificado secundário com o certificado principal.</span><span class="sxs-lookup"><span data-stu-id="2d32f-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![Trocar o certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="2d32f-120">Remover um certificado de cluster usando o portal</span><span class="sxs-lookup"><span data-stu-id="2d32f-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="2d32f-121">Para um cluster seguro, você sempre precisará de, pelo menos, um certificado (primário ou secundário) válido (não revogado ou expirado) implantado; caso contrário, o cluster vai parar de funcionar.</span><span class="sxs-lookup"><span data-stu-id="2d32f-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="2d32f-122">Para remover um certificado secundário sejam usados para segurança de cluster, navegue até a folha de segurança e selecione a opção 'Excluir' no menu de contexto do certificado secundário.</span><span class="sxs-lookup"><span data-stu-id="2d32f-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="2d32f-123">Se sua intenção for remover o certificado que está marcado como primário, você precisará trocá-lo com o secundário primeiro e, em seguida, exclua o secundário após a conclusão da atualização.</span><span class="sxs-lookup"><span data-stu-id="2d32f-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="2d32f-124">Adicionar um certificado secundário usando o Powershell do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d32f-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="2d32f-125">Estas etapas presumem que você esteja familiarizado com o funcionamento do Resource Manager e tenha implantado, pelo menos, um cluster do Service Fabric usando um modelo do Resource Manager e que o modelo usado para configurar o cluster para uso.</span><span class="sxs-lookup"><span data-stu-id="2d32f-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="2d32f-126">Presume-se também que você esteja familiarizado com o uso do JSON.</span><span class="sxs-lookup"><span data-stu-id="2d32f-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="2d32f-127">Se você estiver procurando um modelo de exemplo e parâmetros que você pode usar para acompanhar ou como um ponto de partida, baixe-o deste [repositório Git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="2d32f-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="2d32f-128">Editar o modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d32f-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="2d32f-129">Para facilitar o acompanhamento, o exemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contém todas as edições que faremos.</span><span class="sxs-lookup"><span data-stu-id="2d32f-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="2d32f-130">o exemplo está disponível no [repositório Git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="2d32f-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="2d32f-131">**Certifique-se de seguir todas as etapas**</span><span class="sxs-lookup"><span data-stu-id="2d32f-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="2d32f-132">**Etapa 1:** Abra o modelo do Resource Manager que foi usado para implantar o cluster.</span><span class="sxs-lookup"><span data-stu-id="2d32f-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="2d32f-133">(Se você baixou o exemplo do repositório acima, usar 5-VM-1-NodeTypes-Secure_Step1.JSON para implantar um cluster seguro e, em seguida, abra o modelo).</span><span class="sxs-lookup"><span data-stu-id="2d32f-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="2d32f-134">**Etapa 2:** adicione **dois novos parâmetros** "secCertificateThumbprint" e "secCertificateUrlValue" do tipo "string" para a seção de parâmetro do modelo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="2d32f-135">Você pode copiar o trecho de código a seguir e adicioná-lo ao modelo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="2d32f-136">Dependendo da fonte do seu modelo, você talvez já tenha esses definido, se assim mover para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="2d32f-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
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
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="2d32f-137">**Etapa 3:** faça alterações no recurso **Microsoft.ServiceFabric/clusters** - localize a definição do recurso "Microsoft.ServiceFabric/clusters" em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="2d32f-138">Nas propriedades dessa definição, você encontrará a marcação do JSON “Certificate”, que deve ser parecida com o trecho do JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d32f-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="2d32f-139">Adicione uma nova marcação “thumbprintSecondary” e atribua a ela um valor de “[parameters('secCertificateThumbprint')]”.</span><span class="sxs-lookup"><span data-stu-id="2d32f-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="2d32f-140">Agora a definição de recurso deve ser parecida com a seguinte (dependendo da fonte do modelo, ela poderá não ser exatamente como o trecho abaixo).</span><span class="sxs-lookup"><span data-stu-id="2d32f-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="2d32f-141">Se você quiser **substituir o certificado**, especifique o novo certificado como primário e mover a réplica primária atual como secundário.</span><span class="sxs-lookup"><span data-stu-id="2d32f-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="2d32f-142">Isso resulta na substituição do certificado primário atual pelo novo certificado em uma etapa de implantação.</span><span class="sxs-lookup"><span data-stu-id="2d32f-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="2d32f-143">**Etapa 4:** faça alterações em **todas as** definições de recurso **Microsoft.Compute/virtualMachineScaleSets** – localize a definição do recurso Microsoft.Compute/virtualMachineScaleSets.</span><span class="sxs-lookup"><span data-stu-id="2d32f-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="2d32f-144">Role até "publisher": "Microsoft.Azure.ServiceFabric", em "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="2d32f-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="2d32f-145">Nas configurações de editor do Service Fabric, você verá algo assim.</span><span class="sxs-lookup"><span data-stu-id="2d32f-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="2d32f-147">Adicionar novas entradas de cert a ele</span><span class="sxs-lookup"><span data-stu-id="2d32f-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="2d32f-148">As propriedades devem ter esta aparência</span><span class="sxs-lookup"><span data-stu-id="2d32f-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="2d32f-150">Se você quiser **substituir o certificado**, especifique o novo certificado como primário e mover a réplica primária atual como secundário.</span><span class="sxs-lookup"><span data-stu-id="2d32f-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="2d32f-151">Isso resulta na substituição do certificado atual pelo novo certificado em uma etapa de implantação.</span><span class="sxs-lookup"><span data-stu-id="2d32f-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


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
<span data-ttu-id="2d32f-152">As propriedades devem ter esta aparência</span><span class="sxs-lookup"><span data-stu-id="2d32f-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="2d32f-154">**Etapa 5:** faça alterações em **todas as** definições do recurso **Microsoft.Compute/virtualMachineScaleSets** - localize a definição do recurso Microsoft.Compute/virtualMachineScaleSets.</span><span class="sxs-lookup"><span data-stu-id="2d32f-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="2d32f-155">Role até "vaultCertificates":, em "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="2d32f-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="2d32f-156">O resultado deve ser semelhante a este.</span><span class="sxs-lookup"><span data-stu-id="2d32f-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="2d32f-158">Adicione o secCertificateUrlValue a ele.</span><span class="sxs-lookup"><span data-stu-id="2d32f-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="2d32f-159">use este trecho:</span><span class="sxs-lookup"><span data-stu-id="2d32f-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="2d32f-160">Agora o Json resultante deve ter esta aparência.</span><span class="sxs-lookup"><span data-stu-id="2d32f-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="2d32f-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="2d32f-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="2d32f-162">Repita as etapas 4 e 5 para todas as definições de recurso Nodetypes/Microsoft.Compute/virtualMachineScaleSets em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="2d32f-163">Se você perder um deles, o certificado será instalado naquele VMSS e você terá resultados imprevisíveis em seu cluster, incluindo o cluster ficar inativo (se você terminar com nenhum certificado válido que o cluster possa usar para segurança.</span><span class="sxs-lookup"><span data-stu-id="2d32f-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="2d32f-164">Portanto, verifique, antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2d32f-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="2d32f-165">Edite o arquivo de modelo para refletir os novos parâmetros adicionados acima</span><span class="sxs-lookup"><span data-stu-id="2d32f-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="2d32f-166">Se você estiver usando a amostra do [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) para acompanhar, poderá começar a fazer alterações na amostra 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="2d32f-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="2d32f-167">Editar seu parâmetro de modelo do Resource Manager de arquivo, adicione dois novos parâmetros para secCertificateThumbprint e secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="2d32f-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="2d32f-168">Implantar o modelo no Azure</span><span class="sxs-lookup"><span data-stu-id="2d32f-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="2d32f-169">Agora você está pronto para implantar o modelo no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d32f-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="2d32f-170">Abra um prompt de comando do Azure PS versão 1+.</span><span class="sxs-lookup"><span data-stu-id="2d32f-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="2d32f-171">Faça logon em sua Conta do Azure e selecione a assinatura do Azure específica.</span><span class="sxs-lookup"><span data-stu-id="2d32f-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="2d32f-172">Essa é uma etapa importante para pessoas que têm acesso a mais de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d32f-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="2d32f-173">Teste o modelo antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="2d32f-174">Use o mesmo Grupo de Recursos no qual o cluster está atualmente implantado.</span><span class="sxs-lookup"><span data-stu-id="2d32f-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="2d32f-175">Implante o modelo no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d32f-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="2d32f-176">Use o mesmo Grupo de Recursos no qual o cluster está atualmente implantado.</span><span class="sxs-lookup"><span data-stu-id="2d32f-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="2d32f-177">Execute o comando New-AzureRmResourceGroupDeployment.</span><span class="sxs-lookup"><span data-stu-id="2d32f-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="2d32f-178">Você não precisa especificar o modo, já que o valor padrão é **incremental**.</span><span class="sxs-lookup"><span data-stu-id="2d32f-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="2d32f-179">Se você definir o Modo como Concluído, será possível excluir inadvertidamente os recursos que não estão no modelo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="2d32f-180">Portanto, não o use neste cenário.</span><span class="sxs-lookup"><span data-stu-id="2d32f-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="2d32f-181">Veja um exemplo preenchido do mesmo comando powershell.</span><span class="sxs-lookup"><span data-stu-id="2d32f-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="2d32f-182">Após a conclusão da implantação, conecte-se ao cluster usando o novo Certificado e realize algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="2d32f-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="2d32f-183">Faça isso se conseguir.</span><span class="sxs-lookup"><span data-stu-id="2d32f-183">If you are able to do.</span></span> <span data-ttu-id="2d32f-184">Em seguida, você pode excluir o certificado antigo.</span><span class="sxs-lookup"><span data-stu-id="2d32f-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="2d32f-185">Se estiver usando um certificado autoassinado, não se esqueça de importá-lo para seu repositório de certificados local TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="2d32f-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="2d32f-186">Para referência rápida, este é o comando para se conectar a um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="2d32f-186">For quick reference here is the command to connect to a secure cluster</span></span> 

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
<span data-ttu-id="2d32f-187">Para referência rápida, este é o comando para obter a integridade do cluster</span><span class="sxs-lookup"><span data-stu-id="2d32f-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="2d32f-188">Implantar certificados de aplicativo para o cluster.</span><span class="sxs-lookup"><span data-stu-id="2d32f-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="2d32f-189">Você pode usar as mesmas etapas conforme descrito nas etapas 5 acima para que os certificados implantados de um keyvault para os nós.</span><span class="sxs-lookup"><span data-stu-id="2d32f-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="2d32f-190">apenas é necessário definir e usar parâmetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="2d32f-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="2d32f-191">Adicionando ou removendo certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="2d32f-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="2d32f-192">Além de certificados de cluster, você pode adicionar certificados de cliente para realizar operações de gerenciamento em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2d32f-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="2d32f-193">Você pode adicionar dois tipos de certificados de cliente - Admin ou Somente leitura.</span><span class="sxs-lookup"><span data-stu-id="2d32f-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="2d32f-194">Eles então podem ser usados para controlar o acesso a operações de administração e operações de consulta no cluster.</span><span class="sxs-lookup"><span data-stu-id="2d32f-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="2d32f-195">Por padrão, os certificados de cluster são adicionados à lista de certificados permitida Admin.</span><span class="sxs-lookup"><span data-stu-id="2d32f-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="2d32f-196">Você pode especificar qualquer número de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="2d32f-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="2d32f-197">Cada adição ou exclusão resulta em uma atualização de configuração para o cluster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2d32f-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="2d32f-198">A adição de certificados de cliente - Admin ou somente leitura por meio do portal</span><span class="sxs-lookup"><span data-stu-id="2d32f-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="2d32f-199">Navegue até a folha de segurança e selecione o '+ autenticação' botão na parte superior da folha de segurança.</span><span class="sxs-lookup"><span data-stu-id="2d32f-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="2d32f-200">Na folha ‘Adicionar Autenticação’, escolha o 'Tipo de Autenticação' - 'Cliente somente leitura' ou 'cliente Admin'</span><span class="sxs-lookup"><span data-stu-id="2d32f-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="2d32f-201">Agora, escolha o método de autorização.</span><span class="sxs-lookup"><span data-stu-id="2d32f-201">Now choose the Authorization method.</span></span> <span data-ttu-id="2d32f-202">Indica ao Service Fabric se ele precisa buscar esse certificado usando o nome do assunto ou a impressão digital.</span><span class="sxs-lookup"><span data-stu-id="2d32f-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="2d32f-203">Em geral, não é uma boa prática de segurança para usar o método de autorização do nome da entidade.</span><span class="sxs-lookup"><span data-stu-id="2d32f-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![Adicionar certificado de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="2d32f-205">Exclusão de certificados de cliente - Admin ou somente leitura usando o portal</span><span class="sxs-lookup"><span data-stu-id="2d32f-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="2d32f-206">Para remover um certificado secundário sejam usados para segurança de cluster, navegue até a folha de segurança e selecione a opção 'Excluir' no menu de contexto do certificado específico.</span><span class="sxs-lookup"><span data-stu-id="2d32f-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2d32f-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d32f-207">Next steps</span></span>
<span data-ttu-id="2d32f-208">Leia estes artigos para obter mais informações sobre gerenciamento de cluster:</span><span class="sxs-lookup"><span data-stu-id="2d32f-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="2d32f-209">Processo de atualização de Cluster de Malha do Serviço e as suas expectativas</span><span class="sxs-lookup"><span data-stu-id="2d32f-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="2d32f-210">Configurar o acesso baseado em funções para clientes</span><span class="sxs-lookup"><span data-stu-id="2d32f-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


