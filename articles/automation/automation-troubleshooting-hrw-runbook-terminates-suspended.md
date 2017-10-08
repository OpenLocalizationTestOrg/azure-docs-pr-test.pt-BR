---
title: 'Hybrid Runbook Worker: um trabalho de runbook termina com o status Suspenso | Microsoft Docs'
description: "Sintomas, causas e resoluções para o erro de terminação de trabalho do Hybrid Runbook Worker."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Hybrid Runbook Worker : um trabalho de runbook termina com o status Suspenso
## <a name="summary"></a>Resumo
O runbook for suspenso logo após a tentativa de tooexecute-três vezes. Existem condições que podem interromper a saudação runbook seja concluída com êxito e mensagens de erro relacionadas Olá não incluem qualquer informação adicional que indica o motivo. Este artigo fornece etapas de solução de problemas para falhas de execução de runbook do problemas relacionados toohello Hybrid Runbook Worker.

Se o problema do Azure não é abordado neste artigo, visite Olá fóruns do Azure em [MSDN e Olá estouro de pilha](https://azure.microsoft.com/support/forums/). Você pode lançar seu problema nesses fóruns ou muito[ @AzureSupport no Twitter](https://twitter.com/AzureSupport). Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptom"></a>Sintoma
Falha na execução de runbook e erro Olá retornado é, "hello ação do trabalho 'Activate' não pode ser executado porque Olá processo foi interrompido inesperadamente. ação de saudação do trabalho foi tentada 3 vezes."

## <a name="cause"></a>Causa
Há várias causas possíveis para o erro hello: 

1. hybrid worker de saudação estiver atrás de um proxy ou firewall
2. Olá hybrid worker de saudação do computador está em execução no possui menos que o hardware mínimo Olá [requisitos](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Olá runbooks não pode autenticar com recursos locais

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Causa 1: o Hybrid Runbook Worker está protegido por proxy ou firewall
Olá Olá de computador que Hybrid Runbook Worker está sendo executado no está atrás de um firewall ou servidor proxy e acesso de rede de saída não pode ser permitido ou configurado corretamente.

### <a name="solution"></a>Solução
Verifique se o computador de saudação tem acesso de saída too*.cloudapp .net nas portas 443, 9354 e 30000-30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Causa 2: o computador tem requisitos de hardware inferiores aos mínimos
Computadores que executam o hello Hybrid Runbook Worker devem atender Olá requisitos mínimos de hardware antes de designar a ele toohost esse recurso. Caso contrário, dependendo da utilização de recursos de saudação de outros processos em segundo plano e a contenção provocada por runbooks durante a execução, o computador de hello serão fiquem sobrecarregados e causar tempos limites ou atrasos de trabalho de runbook. 

### <a name="solution"></a>Solução
Confirme primeiro computador Olá designado de recurso do toorun Olá Hybrid Runbook Worker atende aos requisitos de mínimos de hardware de saudação.  Se isso acontecer, monitore toodetermine de utilização de CPU e memória correlação entre desempenho de saudação de processos de trabalho de Runbook híbrido e Windows.  Se não houver memória ou a pressão da CPU, isso pode indicar Olá necessidade tooupgrade ou adicione mais processadores ou aumento de memória tooaddress Olá afunilamento de recurso e resolver o erro de saudação. Como alternativa, selecione um recurso de computação diferentes que pode dar suporte aos requisitos mínimos de hello e escala quando a carga de trabalho indica que um aumento é necessário.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Causa 3: os runbooks não podem ser autenticados com recursos locais
### <a name="solution"></a>Solução
Verificar Olá **Microsoft SMA** log de eventos para um evento correspondente com a descrição *Win32 processo encerrado com código [4294967295]*.  Olá causa esse erro é você ainda não configurou a autenticação em seus runbooks ou Olá executar como as credenciais para o grupo do Hybrid worker Olá especificadas.  Examine [permissões de Runbook](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm você configurou corretamente a autenticação para seus runbooks.  

