---
title: recursos de aaaManage com hello CLI do Azure | Microsoft Docs
description: Use hello Azure Interface de linha de comando (CLI) toomanage Azure recursos e grupos
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="5c31a-103">Usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5c31a-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c31a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5c31a-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="5c31a-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5c31a-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="5c31a-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c31a-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="5c31a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="5c31a-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="5c31a-108">Hello Azure Interface de linha de comando (CLI do Azure) é uma das várias ferramentas, você pode usar toodeploy e gerenciar recursos com o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="5c31a-109">Este artigo apresenta toomanage de maneiras comuns do Azure Olá recursos e grupos de recursos usando a CLI do Azure no modo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="5c31a-110">Para obter informações sobre como usar recursos de toodeploy CLI hello, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="5c31a-111">Para obter informações sobre recursos do Azure e o Gerenciador de recursos, visite Olá [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5c31a-112">toomanage Azure recursos com hello CLI do Azure, você precisa muito[instalar Olá CLI do Azure](../cli-install-nodejs.md), e [login tooAzure](../xplat-cli-connect.md) usando Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="5c31a-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="5c31a-113">Saudação de se tornar CLI está no modo do Gerenciador de recursos (execute `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="5c31a-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="5c31a-114">Se você fez estas coisas, você está pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="5c31a-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="5c31a-115">Obtenha os grupos de recursos e os recursos</span><span class="sxs-lookup"><span data-stu-id="5c31a-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="5c31a-116">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5c31a-116">Resource groups</span></span>
<span data-ttu-id="5c31a-117">tooget uma lista de todos os grupos de recursos em sua assinatura e suas localizações, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="5c31a-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="5c31a-118">Recursos</span><span class="sxs-lookup"><span data-stu-id="5c31a-118">Resources</span></span>
 <span data-ttu-id="5c31a-119">nome de todos os recursos em um grupo, por exemplo, um com toolist *testRG*, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c31a-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="5c31a-120">tooview um recurso individual dentro do grupo de saudação, como uma VM denominada *MyUbuntuVM*, usar um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c31a-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="5c31a-121">Saudação de aviso **Microsoft.Compute/virtualMachines** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5c31a-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="5c31a-122">Esse parâmetro indica o tipo de saudação do recurso Olá em que você está solicitando informações.</span><span class="sxs-lookup"><span data-stu-id="5c31a-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="5c31a-123">Ao usar o hello **recursos do azure** outros comandos além de saudação **lista** de comando, você deve especificar a versão de API de saudação do recurso de saudação com hello **-o** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5c31a-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="5c31a-124">Se você não tiver certeza sobre a versão da API hello, consulte o arquivo de modelo hello e encontrar o campo de apiVersion Olá para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c31a-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="5c31a-125">Para obter mais informações sobre as versões da API no Resource Manager, consulte [Provedores de recursos e tipos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="5c31a-126">Ao exibir detalhes sobre um recurso, geralmente é útil toouse Olá `--json` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5c31a-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="5c31a-127">Esse parâmetro faz saída hello mais legível, pois alguns valores estão estruturas aninhadas ou coleções.</span><span class="sxs-lookup"><span data-stu-id="5c31a-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="5c31a-128">Olá, exemplo a seguir demonstra retornando resultados Olá Olá **Mostrar** comando como um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="5c31a-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="5c31a-129">Se você desejar, salve Olá JSON dados toofile usando Olá &gt; arquivo tooa do caractere toodirect Olá saída.</span><span class="sxs-lookup"><span data-stu-id="5c31a-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="5c31a-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c31a-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="5c31a-131">Marcas</span><span class="sxs-lookup"><span data-stu-id="5c31a-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="5c31a-132">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="5c31a-132">Manage resources</span></span>
<span data-ttu-id="5c31a-133">tooadd um recurso como um grupo de recursos de tooa de conta de armazenamento, execute um comando semelhante a:</span><span class="sxs-lookup"><span data-stu-id="5c31a-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="5c31a-134">Além disso toospecifying Olá versão de API do recurso de saudação com hello **-o** parâmetro, use Olá **-p** cadeia de caracteres do parâmetro toopass um formatada em JSON com quaisquer ou propriedades adicionais.</span><span class="sxs-lookup"><span data-stu-id="5c31a-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="5c31a-135">toodelete um recurso existente, como um recurso de máquina virtual, use um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c31a-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="5c31a-136">toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá **mover recursos do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="5c31a-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="5c31a-137">Olá mostrado no exemplo a seguir como toomove um Cache Redis tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="5c31a-138">Em Olá **-i** parâmetro, forneça uma lista separada por vírgulas de toomove da id de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="5c31a-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="5c31a-139">Tooresources de acesso de controle</span><span class="sxs-lookup"><span data-stu-id="5c31a-139">Control access tooresources</span></span>
<span data-ttu-id="5c31a-140">Você pode usar o hello CLI do Azure toocreate e gerenciar políticas toocontrol acesso tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="5c31a-141">Para obter informações sobre as definições de política e atribuição tooresources de políticas, consulte [usar os recursos de toomanage de política e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="5c31a-142">Por exemplo, definir Olá política toodeny a seguir todas as solicitações em que local não é Oeste dos EUA ou Norte Central dos EUA e salvá-lo toohello policy.json de arquivo de definição de política:</span><span class="sxs-lookup"><span data-stu-id="5c31a-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="5c31a-143">Em seguida, execute Olá **criar definição de política** comando:</span><span class="sxs-lookup"><span data-stu-id="5c31a-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="5c31a-144">Este comando mostra a seguir toohello semelhante saída:</span><span class="sxs-lookup"><span data-stu-id="5c31a-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="5c31a-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="5c31a-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="5c31a-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="5c31a-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="5c31a-147">tooassign uma política no escopo de saudação desejado, use Olá **PolicyDefinitionId** retornado pelo comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5c31a-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="5c31a-148">Em Olá exemplo a seguir, esse escopo é assinatura hello, mas pode definir o escopo de grupos de tooresource ou recursos individuais:</span><span class="sxs-lookup"><span data-stu-id="5c31a-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="5c31a-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="5c31a-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="5c31a-150">Você pode obter, alterar ou remover definições de política usando Olá **Mostrar de definição de política**, **conjunto de definição de política**, e **excluir de definição de política** comandos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="5c31a-151">Da mesma forma, você pode obter, alterar ou remover atribuições de política usando Olá **Mostrar de atribuição de política**, **conjunto de atribuição de política**, e **Excluir atribuição de política** comandos .</span><span class="sxs-lookup"><span data-stu-id="5c31a-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="5c31a-152">Exportar um grupo de recursos como um modelo</span><span class="sxs-lookup"><span data-stu-id="5c31a-152">Export a resource group as a template</span></span>
<span data-ttu-id="5c31a-153">Para um grupo de recursos existente, você pode exibir o modelo do Gerenciador de recursos de Olá Olá para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="5c31a-154">Exportar modelo de saudação oferece dois benefícios:</span><span class="sxs-lookup"><span data-stu-id="5c31a-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="5c31a-155">Você pode facilmente automatizar implantações futuras de solução Olá porque toda a infra-estrutura de saudação é definido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c31a-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="5c31a-156">Você pode se familiarizar com sintaxe do modelo observando Olá JSON que representa sua solução.</span><span class="sxs-lookup"><span data-stu-id="5c31a-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="5c31a-157">Usando Olá CLI do Azure, você pode exportar um modelo que representa o estado atual de saudação do seu grupo de recursos ou baixar Olá modelo que foi usado para uma determinada implantação.</span><span class="sxs-lookup"><span data-stu-id="5c31a-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="5c31a-158">**Exportar modelo Olá para um grupo de recursos** -isso é útil quando você fez alterações tooa grupo de recursos e precisam tooretrieve Olá representação JSON do seu estado atual.</span><span class="sxs-lookup"><span data-stu-id="5c31a-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="5c31a-159">No entanto, o modelo gerado Olá contém apenas um número mínimo de parâmetros e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="5c31a-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="5c31a-160">A maioria dos valores hello no modelo de saudação é codificados.</span><span class="sxs-lookup"><span data-stu-id="5c31a-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="5c31a-161">Antes de implantar o modelo de saudação gerado, talvez você queira tooconvert mais valores hello nos parâmetros e você pode personalizar a implantação Olá para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="5c31a-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="5c31a-162">modelo de saudação tooexport para um recurso grupo tooa diretório local, execute Olá `azure group export` conforme mostrado no exemplo a seguir de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="5c31a-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="5c31a-163">(Substitua seu ambiente do sistema operacional por um diretório local apropriado).</span><span class="sxs-lookup"><span data-stu-id="5c31a-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="5c31a-164">**Baixar modelo de saudação para uma determinada implantação** – isso é útil quando você precisar tooview Olá real do modelo que foi usado toodeploy recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="5c31a-165">modelo de saudação inclui todos os parâmetros e variáveis definidas para a implantação original hello.</span><span class="sxs-lookup"><span data-stu-id="5c31a-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="5c31a-166">No entanto, se alguém na sua organização feita grupo de recursos de toohello alterações fora de definição de saudação no modelo hello, esse modelo não representa estado atual de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c31a-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="5c31a-167">modelo de saudação toodownload usado para um determinada implantação tooa diretório local, execute Olá `azure group deployment template download` comando.</span><span class="sxs-lookup"><span data-stu-id="5c31a-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="5c31a-168">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c31a-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="5c31a-169">A exportação do modelo está na visualização e nem todos os tipos de recursos oferecem suporte atualmente para a exportação de um modelo.</span><span class="sxs-lookup"><span data-stu-id="5c31a-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="5c31a-170">Ao tentar tooexport um modelo, você verá um erro afirmando que alguns recursos não foram exportados.</span><span class="sxs-lookup"><span data-stu-id="5c31a-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="5c31a-171">Se for necessário, defina manualmente esses recursos em seu modelo depois de baixá-lo.</span><span class="sxs-lookup"><span data-stu-id="5c31a-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5c31a-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c31a-172">Next steps</span></span>
* <span data-ttu-id="5c31a-173">detalhes de tooget das operações de implantação e solucionar problemas de erros de implantação com hello CLI do Azure, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="5c31a-174">Se você quiser toouse Olá CLI tooset recursos tooaccess de script ou de um aplicativo, consulte [toocreate CLI do Azure Use uma entidade de serviço tooaccess recursos](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="5c31a-175">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="5c31a-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

