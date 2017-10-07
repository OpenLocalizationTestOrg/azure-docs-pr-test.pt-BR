---
title: "aaaCreate um aplicativo de função da saudação Portal do Azure | Microsoft Docs"
description: "Crie um novo aplicativo de função no serviço de aplicativo do Azure do portal de saudação."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Criar um aplicativo de função do hello portal do Azure

Aplicativos de função do Azure usa a infra-estrutura de serviço de aplicativo do Azure hello. Este tópico mostra como um aplicativo de função no portal do Azure de saudação do toocreate. Um função de aplicativo é o contêiner de saudação que hospeda a execução de saudação de funções individuais. Quando você cria um aplicativo de função no hello plano de hospedagem de serviço de aplicativo, seu aplicativo de função pode usar todos os recursos de saudação do serviço de aplicativo.

## <a name="create-a-function-app"></a>Criar um aplicativo de funções

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Ao criar um aplicativo de funções, forneça um **Nome de aplicativo** válido, que pode conter apenas letras, números e hifens. Sublinhado (**_**) não é um caractere permitido.

Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas. O nome da sua conta de armazenamento deve ser exclusivo no Azure. 

Depois de aplicativo de função hello for criado, você pode criar funções individuais em um ou mais idiomas diferentes. Criar funções [usando o portal de saudação](functions-create-first-azure-function.md#create-function), [implantação contínua](functions-continuous-deployment.md), ou [Carregando com FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Planos de serviço

O Azure Functions tem dois planos de serviço diferentes: o plano de Consumo e o plano do Serviço de Aplicativo. plano de consumo Olá aloca automaticamente a capacidade de computação quando seu código é executado, escalas-out como carga de toohandle necessário e escalas-in quando o código não está em execução. Olá plano de serviço de aplicativo fornece sua função de instalações de saudação de tooall de acesso de aplicativo de serviço de aplicativo. É necessário escolher o plano de serviço quando o aplicativo de funções é criado, e ele não pode ser alterado. Para obter mais informações, consulte [Escolher um plano de hospedagem do Azure Functions](functions-scale.md).

Se você estiver planejando toorun funções de JavaScript em um plano de serviço de aplicativo, você deve escolher um plano com menos núcleos. Para obter mais informações, consulte Olá [referência de JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Requisitos da conta de armazenamento

Ao criar um aplicativo de função no serviço de aplicativo, você deve criar ou vincular tooa uso geral do Azure conta de armazenamento que dá suporte ao armazenamento de Blob, fila e tabela. Internamente, o Functions usa o Armazenamento para operações como gerenciamento de gatilhos e log de execuções de função. Algumas contas de armazenamento não dão suporte a filas e tabelas, como contas de armazenamento somente blob, Armazenamento Premium do Azure e contas de armazenamento de uso geral com replicação ZRS. Essas contas são filtradas fora da folha de conta de armazenamento Olá durante a criação de um aplicativo de função.

>[!NOTE]
>Ao usar o plano de hospedagem de consumo hello, seus arquivos de configuração de código e associação de função são armazenados no armazenamento de arquivo do Azure na conta de armazenamento principal de saudação. Quando você exclui a conta de armazenamento principal hello, esse conteúdo será excluído e não pode ser recuperado.

toolearn mais sobre os tipos de conta de armazenamento, consulte [apresentando os serviços de armazenamento do Azure Olá](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



