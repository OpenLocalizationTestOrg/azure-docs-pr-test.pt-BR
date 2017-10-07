---
title: aaaConfigure um Host do Docker com VirtualBox | Microsoft Docs
description: "Instruções passo a passo tooconfigure padrão Docker instância usando o Docker máquina e VirtualBox"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Configurar um host do Docker com o VirtualBox
## <a name="overview"></a>Visão geral
Este artigo orienta você pela configuração de uma instância de Docker padrão usando a máquina Docker e o VirtualBox. Se você estiver usando Olá [beta do Docker para Windows](http://beta.docker.com/), essa configuração não é necessária.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguintes ferramentas necessário toobe instalado.

* [Caixa de Ferramentas do Docker](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Configurando o cliente do Docker Olá com o Windows PowerShell
tooconfigure um cliente do Docker, simplesmente abra o Windows PowerShell e realize Olá etapas a seguir:

1. Crie uma instância de host do docker padrão.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Verifique se a instância padrão de saudação está configurado e em execução. (Você deve ver uma instância chamada “padrão” em execução.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![saída do docker-machine Is][0]
3. Defina o padrão como host atual hello e configure o shell.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Exiba contêineres do Docker active hello. Olá lista deve estar vazia.
   
    ```PowerShell
    docker ps
    ```
   
    ![saída do docker ps][1]

> [!NOTE]
> Cada vez que você reinicializa o computador de desenvolvimento, você precisará toorestart seu host do docker local.
> toodo, Olá problema comando no prompt de comando a seguir: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
