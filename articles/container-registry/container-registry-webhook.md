---
title: "aaaAzure contêiner do registro webhooks | Microsoft Docs"
description: "Webhooks de registro de contêiner do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, Contêineres, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Usar webhooks de registro de contêiner do Azure – Portal do Azure

Um registro de contêiner do Azure armazena e gerencia imagens de contêiner do Docker privadas, modo toohello semelhante Hub do Docker armazena imagens públicas do Docker. Use o webhooks tootrigger eventos quando certas ações ocorrem em um dos repositórios do registro. Webhooks pode responder tooevents no nível de registro de saudação ou eles podem ser definidos para baixo da marca do repositório específico tooa. 

Para obter mais informações e conceitos, consulte Olá [visão geral](./container-registry-intro.md).

## <a name="prerequisites"></a>Pré-requisitos 

- Registro gerenciado de contêiner do Azure – crie um registro de contêiner gerenciado em sua assinatura do Azure. Por exemplo, usar Olá portal do Azure ou Olá 2.0 do CLI do Azure. 
- Docker CLI - tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instale o mecanismo do Docker. 

## <a name="create-webhook-azure-portal"></a>Criar webhook no portal do Azure

1. Faça logon no portal do Azure de toohello e navegue toohello registro no qual você deseja toocreate webhooks. 

2. Na folha de contêiner Olá, selecione a guia de "Webhooks" hello. 

3. Selecione "Adicionar" hello webhook folha da barra de ferramentas. 

4. Olá completa *Webhook criar* formulário com hello informações a seguir:

| Valor | Descrição |
|---|---|
| Nome | Olá nome toogive toohello webhook. Ele pode conter apenas letras minúsculas e números e entre 5 e 50 caracteres. |
| URI de serviço | Olá URI onde Olá webhook enviar notificações de POSTAGEM. |
| Cabeçalhos personalizados | Cabeçalhos de que deseja toopass junto com a solicitação POST hello. Eles devem estar no formato "chave: valor". |
| Ações de gatilho | Ações que disparam Olá webhook. No momento webhooks podem ser acionados por push e/ou excluir ações tooan imagem. |
| Status | status de saudação do webhook Olá depois que ele é criado. Ele é habilitado por padrão. |
| Escopo | escopo de saudação no que funciona de webhook hello. Por padrão o escopo de saudação é para todos os eventos no registro de saudação. Pode ser especificado para um repositório ou uma marca usando o formato de saudação "repositório: marca". |

Formulário de webhook de exemplo:

![INTERFACE DO USUÁRIO DE DC/SO](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Criar webhook na CLI do Azure

toocreate usando um webhook Olá CLI do Azure, use Olá [criar az acr webhook](/cli/azure/acr/webhook#create) comando.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Testar webhook

### <a name="azure-portal"></a>Portal do Azure

Toousing anterior Olá webhook no contêiner imagem push e ações de exclusão, pode ser testado usando Olá **Ping** botão. Quando usado, Olá Ping envia que um toohello de solicitação post genérico especificado logs e o ponto de extremidade Olá resposta. Isso é útil tooverify que Olá webhook foi configurado corretamente.

1. Selecione webhook Olá deseja tootest. 
2. Na barra de ferramentas superior Olá, selecione a ação de "Ping" hello. 
3. Seleção Olá solicitação e resposta.

### <a name="azure-cli"></a>CLI do Azure

tootest um webhook ACR com hello CLI do Azure, use Olá [ping de webhook acr az](/cli/azure/acr/webhook#ping) comando.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

resultados de saudação toosee, use Olá [az acr lista webhook eventos](/cli/azure/acr/webhook#list-events) comando. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Excluir webhook

### <a name="azure-portal"></a>Portal do Azure

Cada webhook pode ser excluído selecionando webhook hello e botão de exclusão de Olá Olá portal do Azure.

### <a name="azure-cli"></a>CLI do Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```