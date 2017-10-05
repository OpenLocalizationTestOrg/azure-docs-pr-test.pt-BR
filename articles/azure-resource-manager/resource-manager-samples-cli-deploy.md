---
title: "Amostra de Script do CLI do Azure – implantar modelo| Microsoft Docs"
description: Script de exemplo para implantar um modelo do Azure Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 974230f349aec46fde58e69658e05a13bff4296f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---azure-cli-script"></a><span data-ttu-id="4032b-103">Implantação do Azure Resource Manager - script do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4032b-103">Azure Resource Manager template deployment - Azure CLI script</span></span>

<span data-ttu-id="4032b-104">Esse script implanta um modelo do Resource Manager em um grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4032b-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4032b-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4032b-105">Sample script</span></span>

```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
az account set --subscription $subscriptionId

#Check for existing RG
if [ $(az group exists --name $resourceGroupName) == 'false' ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
then
    echo "Template has been successfully deployed"
fi
```

## <a name="clean-up-deployment"></a><span data-ttu-id="4032b-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="4032b-106">Clean up deployment</span></span> 

<span data-ttu-id="4032b-107">Execute o comando a seguir para remover o grupo de recursos e todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="4032b-107">Run the following command to remove the resource group and all its resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4032b-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4032b-108">Script explanation</span></span>

<span data-ttu-id="4032b-109">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="4032b-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="4032b-110">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="4032b-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4032b-111">Command</span><span class="sxs-lookup"><span data-stu-id="4032b-111">Command</span></span> | <span data-ttu-id="4032b-112">Observações</span><span class="sxs-lookup"><span data-stu-id="4032b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4032b-113">az group exists</span><span class="sxs-lookup"><span data-stu-id="4032b-113">az group exists</span></span>](/cli/azure/group#exists) | <span data-ttu-id="4032b-114">Verifica se o grupo de recursos existe.</span><span class="sxs-lookup"><span data-stu-id="4032b-114">Checks whether resource group exists.</span></span> |
| [<span data-ttu-id="4032b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="4032b-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4032b-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4032b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4032b-117">az group deployment create</span><span class="sxs-lookup"><span data-stu-id="4032b-117">az group deployment create</span></span>](/cli/azure/group/deployment#create) | <span data-ttu-id="4032b-118">Inicie uma implantação.</span><span class="sxs-lookup"><span data-stu-id="4032b-118">Start a deployment.</span></span>  |
| [<span data-ttu-id="4032b-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="4032b-119">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="4032b-120">Exclui um grupo de recursos, incluindo todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="4032b-120">Deletes a resource group including all its resources.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="4032b-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4032b-121">Next steps</span></span>
* <span data-ttu-id="4032b-122">Para obter uma introdução à implantação de modelos, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4032b-122">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="4032b-123">Para saber mais sobre como implantar um modelo que exija um token SAS, veja [Implantar o modelo particular com o token SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="4032b-123">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="4032b-124">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="4032b-124">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="4032b-125">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4032b-125">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

