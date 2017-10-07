---
title: aaaDeploy modelo do Azure com o token SAS e a CLI do Azure | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e a CLI do Azure toodeploy tooAzure de recursos de um modelo que está protegido com token SAS."
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
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Implantar o modelo particular do Resource Manager com a CLI do Azure e o token SAS

Quando o modelo estiver em uma conta de armazenamento, você pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso compartilhado durante a implantação. Este tópico explica como toouse PowerShell do Azure com o Gerenciador de recursos modelos tooprovide um token SAS durante a implantação. 

## <a name="add-private-template-toostorage-account"></a>Adicionar modelo particular toostorage conta

Você pode adicionar sua conta de armazenamento tooa modelos e vincular toothem durante a implantação com um token SAS.

> [!IMPORTANT]
> Seguindo as etapas de saudação abaixo, o blob de saudação que contém o modelo de saudação é proprietário da conta Olá tooonly acessível. No entanto, quando você cria um token SAS para blob hello, blob Olá é tooanyone acessível com esse URI. Se outro usuário interceptar Olá URI, esse usuário será capaz de tooaccess modelo de saudação. Usar um token SAS é uma boa maneira de limitar o acesso tooyour modelos, mas você não deve incluir dados confidenciais, como senhas diretamente no modelo de saudação.
> 
> 

Olá exemplo a seguir configura um contêiner de conta de armazenamento privado e carrega um modelo:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Forneça um token SAS durante a implantação
toodeploy um modelo particular em uma conta de armazenamento, gerar um token SAS e incluí-lo em hello URI para o modelo de saudação. Defina tooallow de tempo de expiração Olá suficiente implantação toocomplete hello.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Para ver um exemplo de como usar um token SAS com modelos vinculados, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Próximas etapas
* Para modelos de toodeploying uma introdução, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](resource-group-template-deploy-cli.md).
* Para um script de exemplo completo que implanta um modelo, veja [Implantar o script de modelo do Resource Manager](resource-manager-samples-cli-deploy.md)
* parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).
