---
title: Consumir um aplicativo gerenciado do Azure | Microsoft Docs
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="902a3-103">Consumir um aplicativo gerenciado interno</span><span class="sxs-lookup"><span data-stu-id="902a3-103">Consume an internal managed application</span></span>

<span data-ttu-id="902a3-104">Consuma [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização.</span><span class="sxs-lookup"><span data-stu-id="902a3-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="902a3-105">Por exemplo, selecione os aplicativos gerenciados de seu departamento de TI que garantem a conformidade com os padrões organizacionais.</span><span class="sxs-lookup"><span data-stu-id="902a3-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="902a3-106">Esses aplicativos gerenciados estão disponíveis por meio do Catálogo de Serviços, não pelo Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="902a3-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="902a3-107">Antes de continuar com este artigo, você deve ter um aplicativo gerenciado disponível no catálogo de serviços para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="902a3-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="902a3-108">Se alguém em sua organização ainda não tiver criado um aplicativo gerenciado, consulte [Publicar um aplicativo gerenciado para consumo interno](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="902a3-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="902a3-109">No momento, você pode usar a CLI do Azure ou o portal do Azure para consumir um aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="902a3-110">Criar o aplicativo gerenciado usando o portal</span><span class="sxs-lookup"><span data-stu-id="902a3-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="902a3-111">Para implantar um aplicativo gerenciado por meio do portal, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="902a3-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="902a3-112">Vá para o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="902a3-112">Go to the Azure portal.</span></span> <span data-ttu-id="902a3-113">Pesquise **Aplicativo Gerenciado do Catálogo de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="902a3-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Aplicativo gerenciado do Catálogo de Serviços](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="902a3-115">Selecione o aplicativo gerenciado que você deseja criar na lista de soluções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="902a3-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="902a3-116">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="902a3-116">Select **Create**.</span></span>

   ![Seleção do aplicativo gerenciado](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="902a3-118">Forneça valores para os parâmetros necessários para provisionar os recursos.</span><span class="sxs-lookup"><span data-stu-id="902a3-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="902a3-119">Selecione **Centro-Oeste dos EUA** para local.</span><span class="sxs-lookup"><span data-stu-id="902a3-119">Select **West Central US** for location.</span></span> <span data-ttu-id="902a3-120">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="902a3-120">Select **OK**.</span></span>

   ![Parâmetros do aplicativo gerenciado](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="902a3-122">O modelo valida os valores fornecidos.</span><span class="sxs-lookup"><span data-stu-id="902a3-122">The template validates the values you provided.</span></span> <span data-ttu-id="902a3-123">Se a validação for bem-sucedida, selecione **OK** para iniciar a implantação.</span><span class="sxs-lookup"><span data-stu-id="902a3-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Validação de aplicativo gerenciado](./media/managed-application-consumption/validation.png)

<span data-ttu-id="902a3-125">Depois que a implantação for concluída, os recursos apropriados definidos no modelo serão provisionados no grupo de recursos gerenciado que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="902a3-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="902a3-126">Criar o aplicativo gerenciado usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="902a3-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="902a3-127">Há duas maneiras de criar um aplicativo gerenciado usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="902a3-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="902a3-128">Use o comando para criar aplicativos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="902a3-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="902a3-129">Use o comando de implantação de modelo regular.</span><span class="sxs-lookup"><span data-stu-id="902a3-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="902a3-130">Use o comando de implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="902a3-130">Use the template deployment command</span></span>

<span data-ttu-id="902a3-131">Implante o arquivo applianceMainTemplate.json que o fornecedor criou.</span><span class="sxs-lookup"><span data-stu-id="902a3-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="902a3-132">Depois crie dois grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="902a3-132">Then create two resource groups.</span></span> <span data-ttu-id="902a3-133">O primeiro grupo de recursos é o local em que o recurso de aplicativo gerenciado é criado: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="902a3-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="902a3-134">O segundo grupo de recursos contém todos os recursos definidos em mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="902a3-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="902a3-135">Esse grupo de recursos é gerenciado pelo ISV.</span><span class="sxs-lookup"><span data-stu-id="902a3-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="902a3-136">Use `westcentralus` como o local do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="902a3-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="902a3-137">Para implantar o applianceMainTemplate.json no mainResourceGroup, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="902a3-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="902a3-138">Depois que o modelo anterior é executado, ele solicita os valores dos parâmetros que estão definidos no modelo.</span><span class="sxs-lookup"><span data-stu-id="902a3-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="902a3-139">Além dos parâmetros que são necessários para o provisionamento de recursos em um modelo, você precisa de dois valores de parâmetro principais:</span><span class="sxs-lookup"><span data-stu-id="902a3-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="902a3-140">**managedResourceGroupId**: a ID do grupo de recursos que contém os recursos definidos em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="902a3-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="902a3-141">A ID pertence ao formulário `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="902a3-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="902a3-142">No exemplo anterior, é a ID do `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="902a3-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="902a3-143">**applianceDefinitionId**: A ID do recurso de definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="902a3-144">Esse valor é fornecido pelo ISV.</span><span class="sxs-lookup"><span data-stu-id="902a3-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="902a3-145">O fornecedor deve conceder acesso ao grupo de recursos que contém a definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="902a3-146">O recurso de definição é criado na assinatura do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="902a3-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="902a3-147">Portanto, um usuário, grupo de usuários ou aplicativo no locatário do cliente precisa ter acesso de leitura a esse recurso.</span><span class="sxs-lookup"><span data-stu-id="902a3-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="902a3-148">Depois que a implantação for concluída com êxito, veja se o aplicativo gerenciado foi criado em mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="902a3-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="902a3-149">O recurso storageAccount é criado em managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="902a3-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="902a3-150">Use o comando de criar</span><span class="sxs-lookup"><span data-stu-id="902a3-150">Use the create command</span></span>

<span data-ttu-id="902a3-151">Você pode usar o comando `az managedapp create` para criar um aplicativo gerenciado da definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="902a3-152">**appliance-definition-Id**: a ID do recurso da definição de aplicativo gerenciado criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="902a3-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="902a3-153">Para obter essa ID, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="902a3-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="902a3-154">Esse comando retorna a definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-154">This command returns the managed application definition.</span></span> <span data-ttu-id="902a3-155">Você precisa do valor da propriedade da ID.</span><span class="sxs-lookup"><span data-stu-id="902a3-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="902a3-156">**managed-rg-id**: o nome do grupo de recursos que contém os recursos definidos em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="902a3-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="902a3-157">Esse grupo de recursos é o grupo de recursos gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="902a3-158">Ele é gerenciado pelo editor.</span><span class="sxs-lookup"><span data-stu-id="902a3-158">It's managed by the publisher.</span></span> <span data-ttu-id="902a3-159">Se não existir, ele será criado para você.</span><span class="sxs-lookup"><span data-stu-id="902a3-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="902a3-160">**resource-group**: o grupo de recursos em que o recurso de aplicativo gerenciado é criado.</span><span class="sxs-lookup"><span data-stu-id="902a3-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="902a3-161">O recurso Microsoft.Solutions/appliance reside nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="902a3-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="902a3-162">**parameters**: Os parâmetros necessários para os recursos definidos em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="902a3-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="902a3-163">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="902a3-163">Known issues</span></span>

<span data-ttu-id="902a3-164">Esta versão prévia inclui os seguintes problemas:</span><span class="sxs-lookup"><span data-stu-id="902a3-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="902a3-165">Um erro de servidor interno 500 é exibido durante a criação do aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="902a3-166">Se você tiver esse problema, é provável que ele seja intermitente.</span><span class="sxs-lookup"><span data-stu-id="902a3-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="902a3-167">Repita a operação.</span><span class="sxs-lookup"><span data-stu-id="902a3-167">Retry the operation.</span></span>
* <span data-ttu-id="902a3-168">Um novo grupo de recursos é necessário para o grupo de recursos gerenciado.</span><span class="sxs-lookup"><span data-stu-id="902a3-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="902a3-169">Se for usado um grupo de recursos existente a implantação falha.</span><span class="sxs-lookup"><span data-stu-id="902a3-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="902a3-170">O grupo de recursos que contém o recurso Microsoft.Solutions/appliances deve ser criado na localização **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="902a3-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="902a3-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="902a3-171">Next steps</span></span>

* <span data-ttu-id="902a3-172">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="902a3-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="902a3-173">Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="902a3-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="902a3-174">Para obter informações sobre como publicar aplicativos gerenciados para o Azure Marketplace, consulte [Aplicativos gerenciados do Azure no Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="902a3-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="902a3-175">Para obter informações sobre como consumir um aplicativo gerenciado do Marketplace, consulte [Consumir aplicativos gerenciados pelo Azure no Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="902a3-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
