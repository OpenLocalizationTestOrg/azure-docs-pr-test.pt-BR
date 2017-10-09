---
title: "aaaUse parâmetros de serviço do Azure Machine Learning Web | Microsoft Docs"
description: "Como toouse parâmetros de serviço do Azure Machine Learning Web toomodify Olá comportamento do seu modelo quando o serviço web de saudação é acessado."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Usar os parâmetros do serviço Web de Azure Machine Learning
Um serviço Web de Azure Machine Learning é criado pela publicação de um experimento com módulos com parâmetros configuráveis. Em alguns casos, convém comportamento do módulo Olá toochange enquanto Olá web serviço está em execução. *Parâmetros de serviço de Web* permitem que você toodo essa tarefa. 

Um exemplo comum é configurar Olá [importar dados] [ reader] módulo, portanto, esse usuário Olá Olá publicado serviço web pode especificar uma fonte de dados diferente quando o serviço web de saudação é acessado. Ou configurando Olá [exportar dados] [ writer] módulo para que um destino diferente pode ser especificado. Alguns exemplos incluem a alteração de número de saudação do bits para Olá [hash de recurso] [ feature-hashing] módulo ou hello inúmeros recursos desejados para Olá [seleção de recursos baseada em filtro] [ filter-based-feature-selection] módulo. 

Você pode definir os Parâmetros do Serviço Web e associá-los a um ou mais parâmetros de módulo no seu teste, podendo também especificar se eles são obrigatórios ou opcionais. usuário de saudação do serviço web de hello, em seguida, pode fornecer valores para esses parâmetros quando eles chamam o serviço web de saudação. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Como tooset e usar parâmetros de serviço Web
Você pode definir um parâmetro de serviço Web clicando Olá ícone próximo toohello parâmetro para um módulo e selecionando "Definido como parâmetro de serviço web". Isso cria um novo parâmetro de serviço Web e conecta toothat parâmetro de módulo. Em seguida, quando o serviço web de saudação é acessado, usuário Olá pode especificar um valor para Olá parâmetro do serviço Web e é aplicado toohello parâmetro de módulo.

Depois de definir um parâmetro de serviço da Web, é tooany disponível outro parâmetro de módulo no experimento hello. Se você definir um parâmetro de serviço da Web associada a um parâmetro para um módulo, você pode usar esse mesmo parâmetro de serviço da Web para qualquer outro módulo, como parâmetro hello espera Olá mesmo tipo de valor. Por exemplo, se Olá parâmetro do serviço Web é um valor numérico, ele pode apenas ser usado para parâmetros do módulo que espera um valor numérico. Quando o usuário Olá define um valor para Olá parâmetro de serviço da Web, será aplicado tooall associado parâmetros do módulo.

Você pode decidir se um padrão de tooprovide valor para Olá parâmetro do serviço Web. Se você, em seguida, Olá parâmetro é opcional para o usuário de saudação do serviço web de saudação. Se você não fornecer um valor padrão, o usuário de Olá é necessário tooenter um valor quando o serviço web de saudação é acessado.

Olá documentação da API para o serviço web de saudação inclui informações de usuário do serviço web hello como toospecify Olá parâmetro do serviço Web programaticamente ao acessar o serviço web de saudação.

> [!NOTE]
> Olá documentação da API para um serviço web clássico é fornecido por meio de saudação **página de Ajuda da API** link no serviço da web de saudação **painel** no estúdio de aprendizado de máquina. Olá documentação da API para um novo serviço web é fornecido por meio de saudação [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net/Quickstart) portal Olá **consumir** e **Swagger API** páginas para o serviço da Web.
> 
> 

## <a name="example"></a>Exemplo
Por exemplo, vamos supor que temos um experimento com um [exportar dados] [ writer] módulo que envia o armazenamento de blob tooAzure informações. Vamos definir um parâmetro de serviço da Web denominado "Caminho de Blob" que permite Olá web serviço usuário toochange Olá caminho toohello armazenamento de blob quando o serviço de saudação é acessado.

1. No estúdio de aprendizado de máquina, clique em Olá [exportar dados] [ writer] módulo tooselect-lo. Suas propriedades são mostradas no hello toohello de painel de propriedades à direita da tela de experimento hello.
2. Especifique o tipo de armazenamento hello:
   
   * Em **Especifique o destino de dados**, selecione "Armazenamento de Blobs do Azure".
   * Em **Especifique o tipo de autenticação**, selecione "Conta".
   * Insira informações sobre conta Olá Olá armazenamento de BLOBs do Azure. 
     <p />
3.Clique em toohello de ícone de saudação à direita da saudação **caminho tooblob começando com o parâmetro container**. Ele tem esta aparência:
   
   ![Ícone do Parâmetro de Serviço Web][icon]
   
   Selecione "Definir como parâmetro de serviço Web".
   
   Uma entrada é adicionada sob **parâmetros do Web Service** na parte inferior de saudação do painel de propriedades de saudação com hello nome "caminho tooblob começando com o contêiner". Isso é hello parâmetro do serviço Web que agora está associada a esta [exportar dados] [ writer] parâmetro de módulo.
4. toorename Olá parâmetro do serviço Web, clique Olá nome, digite "Caminho de Blob" e pressione Olá **Enter** chave. 
5. tooprovide um valor padrão para Olá parâmetro de serviço da Web, clique toohello de ícone de saudação à direita do nome de saudação, selecione "Fornecer o valor padrão", insira um valor (por exemplo, "container1/output1.csv") e pressione Olá **Enter** chave.
   
   ![Parâmetro de Serviço Web][parameter]
6. Clique em **Executar**. 
7. Clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]** serviço de web toodeploy hello.

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

usuário de saudação do serviço web de saudação agora pode especificar um novo destino para Olá [exportar dados] [ writer] módulo ao acessar o serviço web de saudação.

## <a name="more-information"></a>Mais informações
Para obter um exemplo mais detalhado, consulte Olá [parâmetros do Web Service](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entrada hello [Blog de aprendizado de máquina](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Para obter mais informações sobre como acessar um serviço da web de aprendizado de máquina, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

