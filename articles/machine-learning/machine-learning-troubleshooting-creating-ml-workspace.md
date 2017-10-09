---
title: "Solução de problemas: Criar e conectar-se o espaço de trabalho de aprendizado de máquina tooa | Microsoft Docs"
description: "Soluções para problemas comuns na criação e conectar-se o espaço de trabalho de aprendizado de máquina do Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Guia de solução de problemas: criar e conectar-se o espaço de trabalho de aprendizado de máquina tooan
Este guia fornece soluções para alguns desafios encontrados com frequência quando você configura espaços de trabalho do Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Proprietário do espaço de trabalho
tooopen um espaço de trabalho no estúdio de aprendizado de máquina, você deve ser conectado toohello Account da Microsoft que você usou o espaço de trabalho do toocreate hello, ou será necessário tooreceive um convite de espaço de trabalho da saudação toojoin Olá proprietário. Olá portal do Azure, você pode gerenciar espaço de trabalho de saudação, que inclui Olá capacidade tooconfigure acesso.

Para obter mais informações sobre como gerenciar um espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Azure Machine Learning].


            [Gerenciar um espaço de trabalho do Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Regiões permitidas
No momento, o Machine Learning está disponível em um número limitado de regiões. Se sua assinatura não tem uma dessas regiões, você poderá ver a mensagem de erro hello, "Você não tem assinaturas em Olá permitido regiões."

toorequest uma região de ser adicionado tooyour assinatura, crie uma nova solicitação de suporte da Microsoft da saudação portal do Azure, escolha **cobrança** como o tipo de problema hello e siga Olá solicita toosubmit sua solicitação.

## <a name="storage-account"></a>Conta de armazenamento
Olá service de aprendizado de máquina precisa de um toostore dados da conta de armazenamento. Você pode usar uma conta de armazenamento existente, ou você pode criar uma nova conta de armazenamento ao criar o espaço de trabalho de aprendizado de máquina de novo hello (se você tiver cota toocreate uma nova conta de armazenamento).

Após a criação do espaço de trabalho de aprendizado de máquina de novo Olá, entrar tooMachine estúdio de aprendizado usando a conta da Microsoft hello usado o espaço de trabalho do toocreate hello. Se você receber a mensagem de erro de hello, "Espaço de trabalho não encontrado" (semelhante toohello captura de tela a seguir), use Olá toodelete as etapas a seguir os cookies do seu navegador.

![Espaço de trabalho não encontrado][screen3]

**cookies do navegador toodelete**

1. Se você usar o Internet Explorer, clique em Olá **ferramentas** botão no canto superior direito de saudação e selecione **opções da Internet**.  

![Opções da Internet][screen4]

2. Em Olá **geral** , clique em **excluir...**

![Guia Geral][screen5]

3. Em Olá **Excluir histórico de navegação** caixa de diálogo caixa, certifique-se de **Cookies e dados de site** está selecionado e clique em **excluir**.

![Excluir cookies][screen6]

Após Olá cookies são excluídos, reinicie o navegador hello e vá toohello [aprendizado de máquina do Microsoft Azure](https://studio.azureml.net) página. Quando você for solicitado, insira um nome de usuário e senha, Olá mesma conta da Microsoft usado o espaço de trabalho do toocreate hello.

## <a name="comments"></a>Comentários

Nosso objetivo é toomake Olá experiência de aprendizado de máquina uniforme possível. Poste quaisquer problemas e comentários no hello [Fórum de aprendizado de máquina do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nos servi-lo melhor.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
