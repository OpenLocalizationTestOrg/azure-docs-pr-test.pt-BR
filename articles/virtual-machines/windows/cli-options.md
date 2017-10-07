---
title: "Olá aaaUsing CLI do Azure no Windows | Microsoft Docs"
description: Usando o hello CLI do Azure no Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Usando o hello CLI do Azure no Windows

Hello Azure Interface de linha de comando (CLI) fornece um ambiente de script para criar e gerenciar recursos do Azure e a linha de comando. Olá CLI do Azure está disponível para sistemas operacionais Windows, Linux e macOS. Entre esses sistemas operacionais, comandos CLI Olá são idênticos, no entanto, sintaxe de script específicas do sistema operacional pode ser diferentes.

Estes documento detalhes Olá maneiras Olá CLI do Azure podem ser instaladas e executadas em Windows e os detalhes de sintáticas considerações para cada. Para ler a documentação detalhada da CLI do Azure, confira a [Documentação da CLI do Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Subsistema do Windows para Linux

Olá subsistema do Windows para Linux (WSL) fornece um ambiente de Ubuntu Linux no Windows 10 aniversário e edições posteriores. Quando habilitado, o WSL fornece uma experiência de Bash nativa, que pode ser usada para criar e executar scripts da CLI do Azure. Como o WSL fornece uma experiência de Bash nativa, os scripts da CLI do Azure podem ser compartilhados entre o macOS, Linux e Windows sem modificação.

Olá toouse CLI do Azure no WSL, execute o seguinte de hello.

|Tarefa | Instruções |
|---|---|
| Habilitar WSL | [Como instalar a documentação de WSL](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Instalar Olá CLI do Azure |[Instalar Olá CLI em WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Olá CLI do Azure pode ser executado nativamente no Windows. Nessa configuração, pacote de CLI do Azure hello está instalado no sistema de operacional do Windows hello e podem ser executados comandos do PowerShell. Nessa configuração, os scripts e os comandos da CLI do Azure podem ser executados em qualquer versão com suporte do Windows, porém você precisará da sintaxe de script específica da plataforma. Por isso, scripts não podem ser necessariamente compartilhados entre macOS, Linux e Windows sem modificação.

Olá toouse CLI do Azure no Windows, instale o pacote de saudação usando estas instruções, [instalação Olá CLI em Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Imagem de Docker

Ao usar o Docker para Windows, uma imagem do Docker pode ser que inclui Olá CLI do Azure iniciada. Essa imagem se baseia no Linux e inclui uma experiência de bash nativa.  Ao usar o Docker para Windows e imagem de CLI do Azure hello, toobe scripts compartilhados entre macOS, Linux e Windows. 

Olá toouse CLI do Azure no Docker para Windows, garantir que o Docker para Windows está em execução e execute Olá comando a seguir.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Depois de concluído, um Bash sessão será iniciado ou seja pré-carregados com ferramentas de CLI do Azure hello.

## <a name="next-steps"></a>Próximas etapas

[Amostra de CLI para máquinas virtuais do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Amostras de CLI para aplicativos Web do Azure](../../app-service-web/app-service-cli-samples.md)

[Amostras de CLI para Azure SQL](../../sql-database/sql-database-cli-samples.md)
