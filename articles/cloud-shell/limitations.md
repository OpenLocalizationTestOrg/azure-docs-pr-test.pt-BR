---
title: "Limitações do Azure Cloud Shell (Visualização) | Microsoft Docs"
description: "Visão geral das limitações do Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitações do Azure Cloud Shell
O Azure Cloud Shell tem as seguintes limitações conhecidas:

## <a name="system-state-and-persistence"></a>Estado do sistema e persistência
O computador que fornece a sessão do Cloud Shell é temporário e é reciclado após a sessão ficar inativa por 20 minutos. O Cloud Shell exige a montagem de um compartilhamento de arquivos. Como resultado, sua assinatura deve ser capaz de configurar recursos de armazenamento para acessar o Cloud Shell. Outras considerações incluem:
* Com o armazenamento montado, apenas as modificações em seu diretório `$Home` ou `clouddrive` são persistidas.
* Os compartilhamentos de arquivo só podem ser montados em sua [região atribuída](persisting-shell-storage.md#mount-a-new-clouddrive).
* Os Arquivos do Azure oferece suporte apenas a armazenamento com redundância local e a contas de armazenamento com redundância geográfica.

## <a name="user-permissions"></a>Permissões de usuário
As permissões são definidas como usuários regulares sem acesso sudo. Qualquer instalação fora do seu diretório `$Home` não será persistida.
Apesar de alguns comandos dentro do diretório `clouddrive`, como `git clone`, não terem as permissões adequadas, seu diretório `$Home` tem essas permissões.

## <a name="browser-support"></a>Suporte ao navegador
O Cloud Shell oferece suporte às versões mais recentes do Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox e Apple Safari. Não há suporte para o Safari no modo particular.

## <a name="copy-and-paste"></a>Copiar e colar
Como Ctrl+C e Ctrl+V não funcionam como atalhos de copiar e colar no Cloud Shell em computadores Windows, use Ctrl+Insert e Shift+Insert para copiar e colar, respectivamente.

As opções de copiar e colar com o botão direito também estão disponíveis, mas a função de clicar com o botão direito está sujeita ao acesso de área de transferência específico de um navegador.

## <a name="editing-bashrc"></a>Edição de .bashrc
Tome cuidado ao editar .bashrc, uma vez que isso pode causar erros inesperados no Cloud Shell.

## <a name="bashhistory"></a>.bash_history
Seu histórico de comandos bash pode ser inconsistente devido a interrupções de sessão a ou sessões simultâneas do Cloud Shell.

## <a name="usage-limits"></a>Limites de uso
O Cloud Shell destina-se a casos de uso interativos. Como resultado, quaisquer sessões não interativo e de longa execução são finalizadas sem aviso.

## <a name="network-connectivity"></a>Conectividade de rede
Qualquer latência no Cloud Shell está sujeita à conectividade de internet local, o Cloud Shell continuará tentando realizar todas as instruções enviadas.

## <a name="next-steps"></a>Próximas etapas
[Início rápido do Cloud Shell](quickstart.md)
