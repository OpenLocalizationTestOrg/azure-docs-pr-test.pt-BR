---
title: "limitações do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitações do Azure Cloud Shell
Shell de nuvem do Azure tem a seguinte Olá limitações conhecidas:

## <a name="system-state-and-persistence"></a>Estado do sistema e persistência
máquina de saudação que fornece sua sessão do Shell de nuvem é temporária e é reciclado depois que a sessão está inativa por 20 minutos. Shell de nuvem requer um toobe de compartilhamento de arquivos montado. Como resultado, sua assinatura deve ser capaz de tooset backup tooaccess de recursos de armazenamento Shell de nuvem. Outras considerações incluem:
* Com o armazenamento montado, apenas as modificações em seu diretório `$Home` ou `clouddrive` são persistidas.
* Os compartilhamentos de arquivo só podem ser montados em sua [região atribuída](persisting-shell-storage.md#mount-a-new-clouddrive).
* Os Arquivos do Azure oferece suporte apenas a armazenamento com redundância local e a contas de armazenamento com redundância geográfica.

## <a name="user-permissions"></a>Permissões de usuário
As permissões são definidas como usuários regulares sem acesso sudo. Qualquer instalação fora do seu diretório `$Home` não será persistida.
Embora determinados comandos dentro Olá `clouddrive` diretório, como `git clone`, não tem permissões adequadas, seu `$Home` diretório tem permissões.

## <a name="browser-support"></a>Suporte ao navegador
Shell de nuvem oferece suporte a versões mais recentes de saudação do Microsoft Internet Explorer, Microsoft Edge, Google Chrome, Mozilla Firefox e Apple Safari. Não há suporte para o Safari no modo particular.

## <a name="copy-and-paste"></a>Copiar e colar
CTRL + C e Ctrl + V não funcionar como copiar/colar atalhos no Shell de nuvem em máquinas do Windows, use Ctrl + Insert e Shift + Insert toocopy e cole respectivamente.

Com o botão direito copiar e colar opções também estão disponíveis, mas função de atalho é acesso de área de transferência toobrowser específicas de assunto.

## <a name="editing-bashrc"></a>Edição de .bashrc
Tome cuidado ao editar .bashrc, uma vez que isso pode causar erros inesperados no Cloud Shell.

## <a name="bashhistory"></a>.bash_history
Seu histórico de comandos bash pode ser inconsistente devido a interrupções de sessão a ou sessões simultâneas do Cloud Shell.

## <a name="usage-limits"></a>Limites de uso
O Cloud Shell destina-se a casos de uso interativos. Como resultado, quaisquer sessões não interativo e de longa execução são finalizadas sem aviso.

## <a name="network-connectivity"></a>Conectividade de rede
Uma latência no Shell de nuvem é a conectividade com a internet toolocal assunto, Shell de nuvem continuará toocarry tooattempt as instruções enviadas.

## <a name="next-steps"></a>Próximas etapas
[Início rápido do Cloud Shell](quickstart.md)
