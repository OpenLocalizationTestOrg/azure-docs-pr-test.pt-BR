---
title: falhas de artefato aaaDiagnose na VM do Azure DevTest Labs | Microsoft Docs
description: Saiba como falhas de artefato de tootroubleshoot em DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Diagnosticar falhas de artefato laboratório Olá 
Depois que você criou um artefato, você pode verificar toosee se ela teve êxito ou falhou. Logs de artefato em DevTest Labs fornecem informações que você pode usar toodiagnose uma falha de artefato. Há duas maneiras diferentes, você pode exibir informações de log de artefato Olá para uma VM do Windows.

> [!NOTE]
> tooensure falhas são identificadas e explicadas, é importante que esse artefato Olá corretamente é estruturado corretamente. Para obter informações sobre como toocorrectly construir um artefato, consulte [criar artefatos personalizados](devtest-lab-artifact-author.md). E toosee um exemplo de um artefato corretamente estruturado, confira esta [tipos de parâmetro de teste](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefato.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Solucionar problemas de falhas de artefato usando Olá portal do Azure
falhas de toodiagnose portal do Azure Olá toouse durante a criação do artefato, siga estas etapas:

1. Na lista de saudação de recursos, selecione seu laboratório.

2. Escolha Olá VM do Windows que inclui o artefato Olá deseja tooinvestigate.

3. No painel esquerdo, Olá em **geral**, escolha **artefatos**. Uma lista de artefatos associados a essa VM é exibida, indicando que nome de saudação do artefato hello e seu status.

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Escolha um artefato que mostra um status **de falha**. artefato Olá é aberto e mostra uma mensagem de extensão que inclui detalhes sobre a falha de saudação do artefato hello.

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Solucionar problemas de falhas de artefato de dentro de saudação VM
logs de artefato de Olá tooview de dentro da máquina virtual de hello, siga estas etapas:

1. Faça logon no toohello VM que contém o artefato Olá toodiagnose desejado.

2. Navegue tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status onde "1.9 é Olá CSE número da versão.

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Olá abrir **status** tooview informações que ajuda a diagnosticar falhas de artefato para a VM do arquivo.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas
* [Ingressar em um domínio de AD usando um modelo do Gerenciador de recursos no Azure DevTest Labs de tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[adicionar um laboratório de tooa repositório Git](devtest-lab-add-artifact-repo.md).

