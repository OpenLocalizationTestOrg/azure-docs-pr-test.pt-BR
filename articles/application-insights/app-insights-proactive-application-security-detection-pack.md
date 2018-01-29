---
title: "Detecção Inteligente - Pacote de Detecção Inteligente com Azure Application Insights | Microsoft Docs"
description: "Monitorar aplicativos com o Azure Application Insights para problemas potenciais de segurança."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: mbullwin
ms.openlocfilehash: 837525d70f28c0710b8a8b86d411a7854402207f
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="application-security-detection-pack-preview"></a>Pacote de detecção de segurança do aplicativo (visualização)

Application Insights analisa automaticamente a telemetria gerada pelo seu aplicativo e detecta possíveis problemas de segurança. Esse recurso permite que você identifique possíveis problemas de segurança e lide com eles, corrigindo o aplicativo ou adotando as medidas de segurança necessárias.

Este recurso não exige nenhuma configuração especial, diferente de [configurar seu aplicativo para enviar telemetria](https://docs.microsoft.com/azure/application-insights/app-insights-usage-overview).

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a>Quando eu receberia este tipo de notificação de detecção inteligente?
Há três tipos de problemas de segurança que são detectados:
1. Acesso de URL não segura: uma URL no aplicativo que está sendo acessada via HTTP e HTTPS. Normalmente, uma URL que aceita solicitações HTTPS não deve aceitar as solicitações HTTP. Isso pode indicar um problema de segurança ou um erro em seu aplicativo.
2. Forma não segura: um formulário (ou outra solicitação de "POST") no aplicativo usa HTTP em vez de HTTPS. Usar HTTP pode comprometer os dados do usuário que são enviados pelo formulário.
3. Atividade de usuário suspeita: o aplicativo está sendo acessado de vários países pelo mesmo usuário em aproximadamente ao mesmo tempo. Por exemplo, o mesmo usuário acessou o aplicativo da Espanha e Estados Unidos na mesma hora. Essa detecção indica uma tentativa de acesso possivelmente mal-intencionado ao seu aplicativo.

## <a name="does-my-app-definitely-have-a-security-issue"></a>Meu aplicativo realmente tem um problema?
Não, uma notificação não significa que seu aplicativo realmente tem um problema. A detecção de qualquer um dos cenários acima pode, em muitos casos, indicar um problema de segurança. No entanto, a detecção pode ter uma justificativa comercial natural e pode ser ignorada.

## <a name="how-do-i-fix-the-insecure-url-access-detection"></a>Como corrigir a detecção de "Acesso à URL inseguro"?
1. **Triagem.** A notificação fornece o número de usuários que acessaram URLs inseguras e a URL que foi mais afetada por acesso inseguro. Isso pode ajudá-lo a atribuir uma prioridade ao problema.
2. **Escopo.** Que porcentagem de usuários acessaram URLs inseguros? Quantos URLs foram afetados? Essas informações podem ser obtidas na notificação.
3. **Diagnosticar.** A detecção fornece a lista de solicitações inseguras e as listas de URLs e os usuários que foram afetados, para ajudá-lo a diagnosticar o problema.

## <a name="how-do-i-fix-the-insecure-form-detection"></a>Como corrigir a detecção de "Formulário inseguro"?
1. **Triagem.** A notificação fornece o número de formulários inseguros e o número de usuários cujos dados foram possivelmente comprometidos. Isso pode ajudá-lo a atribuir uma prioridade ao problema.
2. **Escopo.** Qual forma estava envolvida no maior número de transmissões inseguros e qual é a distribuição de transmissões inseguras, ao longo do tempo? Essas informações podem ser obtidas na notificação.
3. **Diagnosticar.** A detecção fornece a lista de formulários inseguros e uma análise do número de transmissões inseguros para cada formulário, para ajudá-lo a diagnosticar o problema.

## <a name="how-do-i-fix-the-suspicious-user-activity-detection"></a>Como corrigir a detecção de "atividade de usuário suspeita"?
1. **Triagem.** A notificação fornece o número de usuários diferentes que exibiu o comportamento suspeito. Isso pode ajudá-lo a atribuir uma prioridade ao problema.
2. **Escopo.** De quais países as solicitações suspeitas foram originadas? Qual o usuário foi mais suspeito? Essas informações podem ser obtidas na notificação.
3. **Diagnosticar.** A detecção fornece a lista de usuários suspeitos e a lista de países para cada usuário, para ajudá-lo a diagnosticar o problema.
