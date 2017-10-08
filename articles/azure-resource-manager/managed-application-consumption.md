---
title: aplicativo gerenciado de aaaConsume do Azure | Microsoft Docs
description: Descreve como um cliente cria um aplicativo gerenciado do Azure a partir dos arquivos publicados.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="a63c0-103">Consumir um aplicativo gerenciado interno</span><span class="sxs-lookup"><span data-stu-id="a63c0-103">Consume an internal managed application</span></span>

<span data-ttu-id="a63c0-104">Consuma [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização.</span><span class="sxs-lookup"><span data-stu-id="a63c0-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="a63c0-105">Por exemplo, selecione os aplicativos gerenciados de seu departamento de TI que garantem a conformidade com os padrões organizacionais.</span><span class="sxs-lookup"><span data-stu-id="a63c0-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="a63c0-106">Esses aplicativos gerenciados estão disponíveis por meio de saudação catálogo de serviços, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a63c0-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="a63c0-107">Antes de continuar com este artigo, você deve ter um aplicativo gerenciado disponível no catálogo de serviços Olá para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a63c0-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="a63c0-108">Se alguém em sua organização ainda não tiver criado um aplicativo gerenciado, consulte [Publicar um aplicativo gerenciado para consumo interno](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a63c0-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="a63c0-109">No momento, você pode usar a CLI do Azure ou Olá tooconsume portal do Azure um aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="a63c0-110">Criar o aplicativo hello gerenciado usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="a63c0-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="a63c0-111">toodeploy um aplicativo gerenciado por meio do portal hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a63c0-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="a63c0-112">Vá toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a63c0-112">Go toohello Azure portal.</span></span> <span data-ttu-id="a63c0-113">Pesquise **Aplicativo Gerenciado do Catálogo de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="a63c0-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Aplicativo gerenciado do Catálogo de Serviços](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="a63c0-115">Selecione Olá gerenciados aplicativo deseja toocreate da lista de saudação das soluções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a63c0-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="a63c0-116">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a63c0-116">Select **Create**.</span></span>

   ![Seleção do aplicativo gerenciado](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="a63c0-118">Forneça valores para parâmetros de saudação que são necessárias tooprovision Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="a63c0-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="a63c0-119">Selecione **Centro-Oeste dos EUA** para local.</span><span class="sxs-lookup"><span data-stu-id="a63c0-119">Select **West Central US** for location.</span></span> <span data-ttu-id="a63c0-120">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a63c0-120">Select **OK**.</span></span>

   ![Parâmetros do aplicativo gerenciado](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="a63c0-122">modelo de saudação valida valores hello fornecidos.</span><span class="sxs-lookup"><span data-stu-id="a63c0-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="a63c0-123">Se a validação for bem-sucedida, selecione **Okey** toostart implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a63c0-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Validação de aplicativo gerenciado](./media/managed-application-consumption/validation.png)

<span data-ttu-id="a63c0-125">Após a conclusão da implantação hello, os recursos adequados Olá definidos no modelo de saudação são provisionados no grupo de recurso gerenciado Olá fornecida.</span><span class="sxs-lookup"><span data-stu-id="a63c0-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="a63c0-126">Criar um aplicativo hello gerenciado usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a63c0-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="a63c0-127">Há dois toocreate de maneiras um aplicativo gerenciado usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="a63c0-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="a63c0-128">Use o comando Olá para criação de aplicativos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a63c0-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="a63c0-129">Use o comando de implantação de modelo regular hello.</span><span class="sxs-lookup"><span data-stu-id="a63c0-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="a63c0-130">Use o comando de implantação de modelo Olá</span><span class="sxs-lookup"><span data-stu-id="a63c0-130">Use hello template deployment command</span></span>

<span data-ttu-id="a63c0-131">Implante arquivo applianceMainTemplate.json Olá Olá fornecedor criado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="a63c0-132">Depois crie dois grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a63c0-132">Then create two resource groups.</span></span> <span data-ttu-id="a63c0-133">Olá primeiro grupo de recursos é onde hello recursos de aplicativo gerenciado é criado: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="a63c0-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="a63c0-134">segundo grupo de recursos Olá contém todos os recursos de saudação definidos em mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a63c0-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="a63c0-135">Este grupo de recursos é gerenciado pelo Olá ISV.</span><span class="sxs-lookup"><span data-stu-id="a63c0-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="a63c0-136">Use `westcentralus` como local de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a63c0-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="a63c0-137">toodeploy applianceMainTemplate.json em mainResourceGroup, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a63c0-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="a63c0-138">Após Olá anterior é executado de modelo, ele solicitará Olá valores de parâmetros de saudação que são definidos no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a63c0-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="a63c0-139">Além disso toohello parâmetros que são necessários tooprovision recursos em um modelo, você precisa de dois valores de parâmetro de chave:</span><span class="sxs-lookup"><span data-stu-id="a63c0-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="a63c0-140">**managedResourceGroupId**: Olá ID da saudação recurso grupo contentor Olá recursos definidos no applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a63c0-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="a63c0-141">Olá ID tem o formato de saudação `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="a63c0-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="a63c0-142">Em Olá anterior de exemplo, ele do ID de saudação do `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="a63c0-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="a63c0-143">**applianceDefinitionId**: ID de saudação do hello gerenciados recursos de definição de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a63c0-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="a63c0-144">Esse valor é fornecido pelo Olá ISV.</span><span class="sxs-lookup"><span data-stu-id="a63c0-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="a63c0-145">publicador Olá deve conceder o grupo de recursos do acesso toohello que contém a definição do aplicativo hello gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="a63c0-146">recursos de definição de saudação é criado na assinatura do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="a63c0-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="a63c0-147">Portanto, um usuário, grupo de usuário ou aplicativo no locatário de saudação do cliente precisa de acesso de leitura toothis recurso.</span><span class="sxs-lookup"><span data-stu-id="a63c0-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="a63c0-148">Depois de implantação Olá concluída com êxito, você verá Olá gerenciado aplicativo é criado no mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a63c0-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="a63c0-149">recurso de storageAccount de saudação é criado no managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a63c0-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="a63c0-150">Saudação de uso criar comando</span><span class="sxs-lookup"><span data-stu-id="a63c0-150">Use hello create command</span></span>

<span data-ttu-id="a63c0-151">Você pode usar o hello `az managedapp create` comando toocreate um aplicativo gerenciado de saudação gerenciado a definição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a63c0-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="a63c0-152">**ferramenta de definição de Id**: ID de recurso de saudação do hello gerenciado criada no hello anterior da etapa de definição de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a63c0-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="a63c0-153">tooobtain essa ID, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a63c0-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="a63c0-154">Esse comando retorna a definição de aplicativo hello gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="a63c0-155">Você precisa de valor de saudação da propriedade de ID de saudação.</span><span class="sxs-lookup"><span data-stu-id="a63c0-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="a63c0-156">**gerenciado-rg-id**: nome de saudação do hello recurso grupo contentor Olá recursos definidos no applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a63c0-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="a63c0-157">Esse recurso é grupo de recurso gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="a63c0-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="a63c0-158">Ele é gerenciado pelo editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a63c0-158">It's managed by hello publisher.</span></span> <span data-ttu-id="a63c0-159">Se não existir, ele será criado para você.</span><span class="sxs-lookup"><span data-stu-id="a63c0-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="a63c0-160">**grupo de recursos**: grupo de recursos de saudação onde Olá gerenciada recursos de aplicativo é criado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="a63c0-161">Olá Microsoft.Solutions/appliance recurso reside no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a63c0-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="a63c0-162">**parâmetros**: Olá parâmetros que são necessários para os recursos de saudação definidos em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a63c0-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a63c0-163">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="a63c0-163">Known issues</span></span>

<span data-ttu-id="a63c0-164">Esta versão de preview inclui Olá problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a63c0-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="a63c0-165">Um erro de servidor interno 500 é exibido durante a criação de saudação do aplicativo hello gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a63c0-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="a63c0-166">Se você encontrar esse problema, é provável toobe intermitente.</span><span class="sxs-lookup"><span data-stu-id="a63c0-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="a63c0-167">Repita a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a63c0-167">Retry hello operation.</span></span>
* <span data-ttu-id="a63c0-168">Um novo grupo de recursos é necessária para o grupo de recurso gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="a63c0-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="a63c0-169">Se você usar um grupo de recursos existente, a implantação de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="a63c0-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="a63c0-170">Olá grupo de recursos que contém o recurso de Microsoft.Solutions/appliances Olá deve ser criado no hello **westcentralus** local.</span><span class="sxs-lookup"><span data-stu-id="a63c0-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a63c0-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a63c0-171">Next steps</span></span>

* <span data-ttu-id="a63c0-172">Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a63c0-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a63c0-173">Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a63c0-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="a63c0-174">Para obter informações sobre publicação toohello de aplicativos gerenciados do Azure Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a63c0-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="a63c0-175">Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a63c0-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
