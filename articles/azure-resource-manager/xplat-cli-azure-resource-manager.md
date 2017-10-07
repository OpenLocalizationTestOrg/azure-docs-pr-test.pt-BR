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
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [CLI do Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
> 
> 

Hello Azure Interface de linha de comando (CLI do Azure) é uma das várias ferramentas, você pode usar toodeploy e gerenciar recursos com o Gerenciador de recursos. Este artigo apresenta toomanage de maneiras comuns do Azure Olá recursos e grupos de recursos usando a CLI do Azure no modo do Gerenciador de recursos. Para obter informações sobre como usar recursos de toodeploy CLI hello, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](resource-group-template-deploy-cli.md). Para obter informações sobre recursos do Azure e o Gerenciador de recursos, visite Olá [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

> [!NOTE]
> toomanage Azure recursos com hello CLI do Azure, você precisa muito[instalar Olá CLI do Azure](../cli-install-nodejs.md), e [login tooAzure](../xplat-cli-connect.md) usando Olá `azure login` comando. Saudação de se tornar CLI está no modo do Gerenciador de recursos (execute `azure config mode arm`). Se você fez estas coisas, você está pronto toogo.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Obtenha os grupos de recursos e os recursos
### <a name="resource-groups"></a>Grupos de recursos
tooget uma lista de todos os grupos de recursos em sua assinatura e suas localizações, execute este comando.

    azure group list


### <a name="resources"></a>Recursos
 nome de todos os recursos em um grupo, por exemplo, um com toolist *testRG*, use Olá comando a seguir:

    azure resource list testRG

tooview um recurso individual dentro do grupo de saudação, como uma VM denominada *MyUbuntuVM*, usar um comando como Olá a seguir:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Saudação de aviso **Microsoft.Compute/virtualMachines** parâmetro. Esse parâmetro indica o tipo de saudação do recurso Olá em que você está solicitando informações.

> [!NOTE]
> Ao usar o hello **recursos do azure** outros comandos além de saudação **lista** de comando, você deve especificar a versão de API de saudação do recurso de saudação com hello **-o** parâmetro. Se você não tiver certeza sobre a versão da API hello, consulte o arquivo de modelo hello e encontrar o campo de apiVersion Olá para o recurso de saudação. Para obter mais informações sobre as versões da API no Resource Manager, consulte [Provedores de recursos e tipos](resource-manager-supported-services.md).
> 
> 

Ao exibir detalhes sobre um recurso, geralmente é útil toouse Olá `--json` parâmetro. Esse parâmetro faz saída hello mais legível, pois alguns valores estão estruturas aninhadas ou coleções. Olá, exemplo a seguir demonstra retornando resultados Olá Olá **Mostrar** comando como um documento JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Se você desejar, salve Olá JSON dados toofile usando Olá &gt; arquivo tooa do caractere toodirect Olá saída. Por exemplo:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Marcas
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Gerenciar recursos
tooadd um recurso como um grupo de recursos de tooa de conta de armazenamento, execute um comando semelhante a:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Além disso toospecifying Olá versão de API do recurso de saudação com hello **-o** parâmetro, use Olá **-p** cadeia de caracteres do parâmetro toopass um formatada em JSON com quaisquer ou propriedades adicionais.

toodelete um recurso existente, como um recurso de máquina virtual, use um comando como Olá a seguir:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá **mover recursos do azure** comando. Olá mostrado no exemplo a seguir como toomove um Cache Redis tooa novo grupo de recursos. Em Olá **-i** parâmetro, forneça uma lista separada por vírgulas de toomove da id de recurso hello.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Tooresources de acesso de controle
Você pode usar o hello CLI do Azure toocreate e gerenciar políticas toocontrol acesso tooAzure recursos. Para obter informações sobre as definições de política e atribuição tooresources de políticas, consulte [usar os recursos de toomanage de política e controlar o acesso](resource-manager-policy.md).

Por exemplo, definir Olá política toodeny a seguir todas as solicitações em que local não é Oeste dos EUA ou Norte Central dos EUA e salvá-lo toohello policy.json de arquivo de definição de política:

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

Em seguida, execute Olá **criar definição de política** comando:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Este comando mostra a seguir toohello semelhante saída:

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 tooassign uma política no escopo de saudação desejado, use Olá **PolicyDefinitionId** retornado pelo comando anterior hello. Em Olá exemplo a seguir, esse escopo é assinatura hello, mas pode definir o escopo de grupos de tooresource ou recursos individuais:

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

Você pode obter, alterar ou remover definições de política usando Olá **Mostrar de definição de política**, **conjunto de definição de política**, e **excluir de definição de política** comandos.

Da mesma forma, você pode obter, alterar ou remover atribuições de política usando Olá **Mostrar de atribuição de política**, **conjunto de atribuição de política**, e **Excluir atribuição de política** comandos .

## <a name="export-a-resource-group-as-a-template"></a>Exportar um grupo de recursos como um modelo
Para um grupo de recursos existente, você pode exibir o modelo do Gerenciador de recursos de Olá Olá para grupo de recursos. Exportar modelo de saudação oferece dois benefícios:

1. Você pode facilmente automatizar implantações futuras de solução Olá porque toda a infra-estrutura de saudação é definido no modelo de saudação.
2. Você pode se familiarizar com sintaxe do modelo observando Olá JSON que representa sua solução.

Usando Olá CLI do Azure, você pode exportar um modelo que representa o estado atual de saudação do seu grupo de recursos ou baixar Olá modelo que foi usado para uma determinada implantação.

* **Exportar modelo Olá para um grupo de recursos** -isso é útil quando você fez alterações tooa grupo de recursos e precisam tooretrieve Olá representação JSON do seu estado atual. No entanto, o modelo gerado Olá contém apenas um número mínimo de parâmetros e nenhuma variável. A maioria dos valores hello no modelo de saudação é codificados. Antes de implantar o modelo de saudação gerado, talvez você queira tooconvert mais valores hello nos parâmetros e você pode personalizar a implantação Olá para ambientes diferentes.
  
    modelo de saudação tooexport para um recurso grupo tooa diretório local, execute Olá `azure group export` conforme mostrado no exemplo a seguir de saudação do comando. (Substitua seu ambiente do sistema operacional por um diretório local apropriado).
  
        azure group export testRG ~/azure/templates/
* **Baixar modelo de saudação para uma determinada implantação** – isso é útil quando você precisar tooview Olá real do modelo que foi usado toodeploy recursos. modelo de saudação inclui todos os parâmetros e variáveis definidas para a implantação original hello. No entanto, se alguém na sua organização feita grupo de recursos de toohello alterações fora de definição de saudação no modelo hello, esse modelo não representa estado atual de Olá Olá do grupo de recursos.
  
    modelo de saudação toodownload usado para um determinada implantação tooa diretório local, execute Olá `azure group deployment template download` comando. Por exemplo:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> A exportação do modelo está na visualização e nem todos os tipos de recursos oferecem suporte atualmente para a exportação de um modelo. Ao tentar tooexport um modelo, você verá um erro afirmando que alguns recursos não foram exportados. Se for necessário, defina manualmente esses recursos em seu modelo depois de baixá-lo.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* detalhes de tooget das operações de implantação e solucionar problemas de erros de implantação com hello CLI do Azure, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
* Se você quiser toouse Olá CLI tooset recursos tooaccess de script ou de um aplicativo, consulte [toocreate CLI do Azure Use uma entidade de serviço tooaccess recursos](resource-group-authenticate-service-principal-cli.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

