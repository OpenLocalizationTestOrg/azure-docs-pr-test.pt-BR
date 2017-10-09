---
title: "um espaço de trabalho do aprendizado de máquina do aaaCreate | Microsoft Docs"
description: "Como toocreate um espaço de trabalho para o estúdio de aprendizado de máquina do Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Criar e compartilhar um espaço de trabalho de Azure Machine Learning
Esse menu links tootopics que descrevem como tooset backup Olá vários ambientes de ciência de dados usado pelo Olá processo de análise da Cortana (CAPS).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse estúdio de aprendizado de máquina do Azure, você precisa toohave um espaço de trabalho do aprendizado de máquina. Este espaço de trabalho contém ferramentas Olá necessárias toocreate, gerenciar e publicar experiências.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate um espaço de trabalho
1. Entrar toohello [portal do Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign em e criar um espaço de trabalho, você precisa toobe um administrador de assinatura do Azure. 
    >
    > 

2. Clique em **+Novo**

3. Selecione **Inteligência + análise**, clique em **Espaço de Trabalho do Machine Learning**, e clique em **Criar**

4. Insira suas informações de espaço de trabalho

    - Olá *nome do espaço de trabalho* pode ser too260 caracteres, não termine em um espaço. nome de saudação não pode incluir estes caracteres:`< > * % & : \ ? + /`
    - Olá *plano do serviço web* você escolher (ou criar), juntamente com hello associado *preço* você selecionar, será usado se você implantar serviços web deste espaço de trabalho.

    ![Criar um novo espaço de trabalho](media/machine-learning-create-workspace/create-new-workspace.png)

5. Clique em **Criar**

Depois que o espaço de trabalho de saudação é implantado, você pode abri-lo no estúdio de aprendizado de máquina.

1. Procurar tooMachine estúdio de aprendizado em [https://studio.azureml.net/](https://studio.azureml.net/).

2. Selecione o espaço de trabalho no canto de superior direito da saudação.

    ![Selecione o espaço de trabalho](media/machine-learning-create-workspace/open-workspace.png)

3. Clique em **meus experimentos**.

    ![Experimentos abertos](media/machine-learning-create-workspace/my-experiments.png)

Para saber mais sobre como gerenciar seu espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Azure Machine Learning](machine-learning-manage-workspace.md).
Se você encontrar um problema ao criar seu espaço de trabalho, consulte [guia de solução de problemas: criar e conectar-se o espaço de trabalho de aprendizado de máquina tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Compartilhar um espaço de trabalho do Azure Machine Learning
Depois de criar um espaço de trabalho do aprendizado de máquina, você pode convidar usuários tooyour espaço de trabalho tooshare acesso tooyour espaço de trabalho e todas as suas experiências, conjuntos de dados, anotações, etc. Você pode adicionar usuários em uma das duas funções:

* **Usuário** -um usuário do espaço de trabalho pode criar, abrir, modificar e excluir experiências, conjuntos de dados, etc. no espaço de trabalho de saudação.
* **Proprietário** - um proprietário pode convidar e remover usuários no espaço de trabalho hello, na inclusão toowhat um usuário podem fazer.

> [!NOTE]
> conta de administrador de saudação que cria o espaço de trabalho de saudação é automaticamente adicionada toohello espaço de trabalho como proprietário do espaço de trabalho. No entanto, outros administradores ou usuários de assinatura não são automaticamente concedido acesso toohello espaço de trabalho - você precisa tooinvite-los explicitamente.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare um espaço de trabalho

1. Entrar tooMachine estúdio de aprendizado em [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. No painel esquerdo do hello, clique em **configurações**

3. Clique em Olá **usuários** guia

4. Clique em **CONVIDAR usuários mais** final Olá Olá página

    ![Configurações do Studio](media/machine-learning-create-workspace/settings.png)

5. Insira um ou mais endereços de email. usuários de saudação precisam de uma conta da Microsoft válida ou uma conta organizacional (a partir do Active Directory do Azure).

6. Selecione se deseja que os usuários de saudação do tooadd como proprietário ou usuário.

7. Clique em Olá **Okey** botão de marca de seleção.

Cada usuário que você adicionar receberá um email com instruções sobre como toosign no toohello compartilhados espaço de trabalho.

> [!NOTE]
> Para usuários toobe capaz de toodeploy ou gerenciar os serviços web neste espaço de trabalho, eles devem ser um administrador no hello assinatura do Azure ou colaborador. 



