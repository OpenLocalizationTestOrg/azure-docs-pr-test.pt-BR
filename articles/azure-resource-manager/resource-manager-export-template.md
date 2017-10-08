---
title: modelo do Gerenciador de recursos do Azure aaaExport | Microsoft Docs
description: Use o gerenciamento de recursos do Azure tooexport um modelo de um grupo de recursos existente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Exportar um modelo do Azure Resource Manager a partir dos recursos existentes
Neste artigo, você aprenderá como tooexport um modelo do Gerenciador de recursos de recursos existentes em sua assinatura. Você pode usar esse toogain modelo gerado uma melhor compreensão da sintaxe de modelo.

Há dois tooexport de maneiras de um modelo:

* Você pode exportar Olá **real usado para implantação do modelo**. modelo exportado Olá inclui todas as variáveis e parâmetros de saudação exatamente como eles eram exibidos no modelo original hello. Essa abordagem é útil quando você implantou recursos por meio do portal hello e deseja toosee Olá modelo toocreate esses recursos. Este modelo é facilmente utilizável. 
* Você pode exportar um **gerado do modelo que representa o estado atual de saudação do grupo de recursos de saudação**. modelo exportado Olá não é baseado em qualquer modelo que você usou para a implantação. Em vez disso, ele cria um modelo que é um instantâneo de saudação do grupo de recursos. modelo exportado Olá tem muitos valores embutidos e provavelmente não tantos parâmetros quantos você definiria normalmente. Essa abordagem é útil quando você modificou o grupo de recursos de saudação após a implantação. Este modelo geralmente requer modificações antes de ser usado.

Este tópico mostra ambas as abordagens por meio do portal hello.

## <a name="deploy-resources"></a>Implantação de recursos
Vamos começar tooAzure de recursos que você pode usar para exportar como um modelo de implantação. Se você já tiver um grupo de recursos em sua assinatura que você deseja tooexport tooa modelo, você poderá ignorar esta seção. Olá restante deste artigo presume que você implantou Olá web app e solução de banco de dados SQL mostrados nesta seção. Se você usar uma solução diferente, sua experiência pode ser um pouco diferente, mas etapas Olá tooexport um modelo são Olá mesmo. 

1. Em Olá [portal do Azure](https://portal.azure.com), selecione **novo**.
   
      ![Selecione Novo](./media/resource-manager-export-template/new.png)
2. Procurar **web app + SQL** e selecioná-lo entre as opções disponíveis de saudação.
   
      ![Pesquise aplicativo Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Selecione **Criar**.

      ![Selecione Criar](./media/resource-manager-export-template/create.png)

4. Forneça valores de saudação necessária para Olá web app e o banco de dados SQL. Selecione **Criar**.

      ![Forneça a web e o valor SQL](./media/resource-manager-export-template/provide-web-values.png)

implantação de saudação pode levar um minuto. Após a conclusão da implantação hello, sua assinatura contém solução hello.

## <a name="view-template-from-deployment-history"></a>Visualização de modelo do histórico de implantações
1. Vá toohello folha de grupo de recursos para seu novo grupo de recursos. Observe a que folha Olá mostra o resultado de saudação da última implantação de saudação. Selecione este link.
   
      ![folha do grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. Você ver um histórico de implantações de grupo hello. No seu caso, a folha Olá provavelmente lista apenas uma implantação. Selecione essa implantação.
   
     ![última implantação](./media/resource-manager-export-template/select-history.png)
3. folha de saudação exibe um resumo de implantação de saudação. Olá resumo inclui o status de saudação da implantação de saudação e suas operações e valores hello fornecido para os parâmetros. modelo de saudação toosee que você usou para a implantação de saudação, selecione **exibir modelo**.
   
     ![exibir resumo da implantação](./media/resource-manager-export-template/view-template.png)
4. Gerenciador de recursos recupera Olá sete arquivos a seguir para você:
   
   1. **Modelo** -modelo Olá que define a infraestrutura de saudação para sua solução. Quando você criou a conta de armazenamento Olá por meio do portal Olá, Gerenciador de recursos usado um modelo toodeploy-lo e salva esse modelo para referência futura.
   2. **Parâmetros** -um arquivo de parâmetro que você pode usar toopass em valores de durante a implantação. Contém valores hello que você forneceu durante a implantação de saudação primeiro. Você pode alterar qualquer um desses valores ao reimplantar o modelo de saudação.
   3. **CLI** -arquivo de script do Azure de uma interface de linha comando (CLI) que você pode usar o modelo de saudação toodeploy.
   3. **2.0 do CLI** -arquivo de script do Azure de uma interface de linha comando (CLI) que você pode usar o modelo de saudação toodeploy.
   4. **PowerShell** -arquivo de script de um Azure PowerShell que você pode usar o modelo de saudação toodeploy.
   5. **.NET** -classe .NET A que você pode usar o modelo de saudação toodeploy.
   6. **Ruby** -classe Ruby A que você pode usar o modelo de saudação toodeploy.
      
      arquivos de saudação estão disponíveis por meio de links em folha hello. Por padrão, a folha de saudação exibe modelo hello.
      
       ![Exibir modelo](./media/resource-manager-export-template/see-template.png)
      
Este modelo é modelo real Olá usado toocreate seu aplicativo web e o banco de dados SQL. Observe que ele contém parâmetros que permitem valores diferentes de tooprovide durante a implantação. toolearn mais sobre a estrutura de saudação de um modelo, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Exportar modelo de saudação do grupo de recursos
Se você tiver manualmente seus recursos alterados ou adicionados recursos em várias implantações, recuperando um modelo de histórico de implantação Olá refletem não o estado atual de Olá Olá do grupo de recursos. Esta seção mostra como tooexport um modelo que reflete Olá o estado atual do grupo de recursos de saudação. 

> [!NOTE]
> Você não pode exportar um modelo para um grupo de recursos que tenha mais de 200 recursos.
> 
> 

1. modelo de saudação tooview para um grupo de recursos, selecione **script de automação**.
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     Gerenciador de recursos avalia Olá recursos no grupo de recursos de saudação e gera um modelo para esses recursos. Nem todos os tipos de recurso suportam Olá exportar modelo de função. Você verá um erro indicando que há um problema com a exportação de saudação. Você aprenderá como toohandle os problemas no hello [correção de problemas de exportação](#fix-export-issues) seção.
2. Novamente, verá que você pode usar a solução de saudação tooredeploy seis arquivos de saudação. No entanto, esse modelo de saudação do tempo é um pouco diferente. Observe que Olá modelo gerado contém menos parâmetros do modelo de saudação na seção anterior. Além disso, muitos dos valores da saudação (como o local e valores SKU) são codificados por este modelo em vez de aceitar um valor de parâmetro. Antes de reutilizar esse modelo, talvez você queira tooedit Olá modelo toomake melhor uso de parâmetros. 
   
3. Você tem duas opções para continuar toowork com esse modelo. Você pode baixar o modelo hello e executá-la localmente com um editor de JSON. Ou, você pode salvar a biblioteca de tooyour modelo hello e trabalhar por meio do portal hello.
   
     Se você estiver familiarizado com o uso de um editor de JSON como [código VS](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), talvez você prefira baixar modelo de saudação localmente e usar esse editor. toowork localmente, selecione **baixar**.
   
      ![baixar modelo](./media/resource-manager-export-template/download-template.png)
   
     Se você não estiver configurado com um editor de JSON, talvez você prefira editando Olá modelo por meio do portal hello. Olá restante este tópico presume que você salvou biblioteca de tooyour Olá modelos no portal de saudação. No entanto, você fazer Olá mesmo modelo toohello alterações de sintaxe se trabalhando localmente com um editor de JSON ou por meio do portal hello. Selecione toowork por meio do portal hello, **adicionar toolibrary**.
   
      ![Adicionar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Ao adicionar uma biblioteca de toohello de modelo, atribua o modelo de saudação um nome e uma descrição. Em seguida, selecione **Salvar**.
   
     ![definir valores de modelo](./media/resource-manager-export-template/save-library-template.png)
4. tooview um modelo de salvo em sua biblioteca, selecione **mais serviços**, tipo **modelos** toofilter resultados, selecionados **modelos**.
   
      ![localizar modelos](./media/resource-manager-export-template/find-templates.png)
5. Selecione o modelo de saudação com nome hello que você salvou.
   
      ![selecionar modelo](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Personalizar o modelo de saudação
trabalha de modelo Hello exportada bem que se você quiser toocreate Olá mesmo web app e o banco de dados SQL para cada implantação. No entanto, o Resource Manager fornece opções para que você possa implantar modelos com muito mais flexibilidade. Este artigo mostra como parâmetros de tooadd para Olá banco de dados nome do administrador e senha. Você pode usar esse mesmo tooadd de abordagem mais flexibilidade para outros valores no modelo de saudação.

1. modelo de saudação toocustomize, selecione **editar**.
   
     ![mostrar modelo](./media/resource-manager-export-template/select-edit.png)
2. Selecione o modelo de saudação.
   
     ![editar modelo](./media/resource-manager-export-template/select-added-template.png)
3. valores de saudação do toobe toopass capaz de que talvez você queira toospecify durante a implantação, adicione Olá toohello de dois parâmetros a seguir **parâmetros** seção modelo hello:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse Olá novos parâmetros, substituir definição Olá SQL server no hello **recursos** seção. Observe que o **administratorLogin** e o **administratorLoginPassword** passaram a usar os valores de parâmetros.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Selecione **Okey** quando tiver terminado a edição de modelo de saudação.
7. Selecione **salvar** modelo de toohello toosave Olá alterações.
   
     ![salvar modelo](./media/resource-manager-export-template/save-template.png)
8. modelo de saudação atualizado tooredeploy, selecione **implantar**.
   
     ![implantar modelo](./media/resource-manager-export-template/redeploy-template.png)
9. Fornecer valores de parâmetro e selecione um recurso de saudação do recurso grupo toodeploy para.


## <a name="fix-export-issues"></a>Corrigir os problemas da exportação
Nem todos os tipos de recurso suportam Olá exportar modelo de função. tooresolve manualmente esse problema, adicione recursos ausentes Olá volta para o modelo. mensagem de erro de saudação inclui tipos de recurso de saudação não podem ser exportados. Encontre o tipo de recurso em [referência de modelo](/azure/templates/). Por exemplo, toomanually adicionar um gateway de rede virtual, consulte [referência de modelo Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Você só encontra problemas de exportação quando exporta de um grupo de recursos em vez de seu histórico de implantações. Se sua última implantação representa com precisão o estado atual de Olá Olá do grupo de recursos, você deve exportar modelo de saudação do histórico de implantação de saudação em vez de saudação do grupo de recursos. Exporte somente de um grupo de recursos quando você tiver feito alterações toohello grupo de recursos não estão definidas em um único modelo.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Você aprendeu como tooexport um modelo de recursos que você criou no portal de saudação.

* Você pode implantar um modelo por meio do [PowerShell](resource-group-template-deploy.md), da [CLI do Azure](resource-group-template-deploy-cli.md) ou da [API REST](resource-group-template-deploy-rest.md).
* toosee como tooexport um modelo por meio do PowerShell, consulte [usando o PowerShell do Azure com o Azure Resource Manager](powershell-azure-resource-manager.md).
* toosee como tooexport um modelo por meio da CLI do Azure, consulte [Olá Use CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).

