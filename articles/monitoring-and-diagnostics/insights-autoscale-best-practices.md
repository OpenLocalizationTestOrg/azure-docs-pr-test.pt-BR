---
title: "práticas recomendadas de aaaBest para dimensionamento automático | Microsoft Docs"
description: "Padrões de dimensionamento automático no Azure para Aplicativos Web, conjuntos de Dimensionamento de Máquina Virtual e Serviços de Nuvem"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Práticas recomendadas para Dimensionamento Automático
Este artigo ensina tooautoscale de práticas recomendada no Azure. Dimensionamento automático de Monitor do Azure se aplica apenas muito[conjuntos de escala de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/), e [do serviço de aplicativo - aplicativos Web](https://azure.microsoft.com/services/app-service/web/). Outros serviços do Azure usam métodos de dimensionamento diferentes.

## <a name="autoscale-concepts"></a>Conceitos de dimensionamento automático
* Um recurso pode ter apenas *uma* configuração de Dimensionamento Automático
* Uma configuração de Dimensionamento Automático pode ter um ou mais perfis e cada perfil pode ter uma ou mais regras de dimensionamento automático.
* Uma configuração de AutoEscala dimensiona instâncias horizontalmente, que é *out* aumentando instâncias hello e *em* , diminuindo o número de saudação de instâncias.
  Uma configuração de dimensionamento automático tem um valor máximo, mínimo e padrão de instâncias.
* Um trabalho de dimensionamento automático sempre lê Olá associados tooscale métrica, verificando se ele tem ultrapassou o limite configurado de saudação para expansão ou escala no. Você pode exibir uma lista de métricas que o dimensionamento automático pode dimensionar em [métricas comuns de dimensionamento automático do Azure Monitor](insights-autoscale-common-metrics.md).
* Todos os limites são calculados em um nível de instância. Por exemplo, "escala fora por 1 instância quando médio da CPU > 80% quando a contagem de instâncias é 2", significa expansão quando Olá média de CPU em todas as instâncias é maior do que 80%.
* Você sempre receberá notificações de falha via email. Especificamente, o proprietário hello, Colaborador e leitores do recurso de destino Olá recebem email. Você também receberá um email de *recuperação* quando o dimensionamento automático se recuperar de uma falha e iniciar o funcionamento normalmente.
* Você pode participar tooreceive uma notificação de ação de escala com êxito por meio de email e webhooks.

## <a name="autoscale-best-practices"></a>Práticas recomendadas de dimensionamento automático
Use Olá seguir as práticas recomendadas ao usar o dimensionamento automático.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Verifique os valores mínimo e máximo Olá são diferentes e tem uma margem suficiente entre eles
Se você tiver uma configuração que tenha o mínimo = 2, máximo = 2 e a contagem atual de instâncias de saudação é 2, nenhuma ação de escala pode ocorrer. Manter uma margem suficiente entre contagens de instância máximo e mínimo hello, que são inclusivos. O dimensionamento automático sempre dimensiona dentro desses limites.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>O redimensionamento manual é redefinido pelo máximo e pelo mínimo do dimensionamento automático
Se você atualizar Olá instância contagem tooa valor acima ou abaixo do máximo de Olá Olá AutoEscala mecanismo automaticamente manualmente dimensiona back toohello mínimo (se abaixo) ou hello máximo (se estiver acima). Por exemplo, você define o intervalo de saudação entre 3 e 6. Se você tiver uma instância em execução, o mecanismo de dimensionamento automático Olá dimensiona too3 instâncias na sua próxima execução. Da mesma forma, ele seria escala-in 8 instâncias fazer too6 na sua próxima execução.  Redimensionamento manual é muito temporária, a menos que você redefina regras de AutoEscala Olá também.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Sempre use uma combinação de regras de escala e redução horizontal que executa um aumento e uma redução
Se você usar apenas uma parte da combinação de hello, AutoEscala escala-in se o único limite ou, até Olá máximo ou mínimo, é atingido.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Não alternar entre Olá portal do Azure e hello portal clássico do Azure ao gerenciar o dimensionamento automático
Para serviços de nuvem e serviços de aplicativos (aplicativos da Web), use Olá portal do Azure (portal.azure.com) toocreate e gerenciar configurações de dimensionamento automático. Para conjuntos de escala de máquina Virtual use toocreate PowerShell, CLI ou API REST e gerenciar a configuração de dimensionamento automático. Não alterne entre Olá portal clássico do Azure (manage.windowsazure.com) e hello (portal.azure.com) do portal do Azure ao gerenciar configurações de dimensionamento automático. Olá portal clássico do Azure e seu back-end subjacente tem limitações. Mova toohello toomanage portal do Azure AutoEscala usando uma interface gráfica do usuário. Opções de saudação são toouse Olá AutoEscala PowerShell, CLI ou API REST (por meio do Gerenciador de recursos do Azure).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Escolha a estatística de saudação apropriado para sua métrica de diagnóstico
Para métricas de diagnóstico, você pode escolher entre *médio*, *mínimo*, *máximo* e *Total* como uma métrica tooscale por. estatística de Hello mais comum é *médio*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Escolha os limites de saudação cuidadosamente para todos os tipos de métrica
Recomendamos escolher cuidadosamente limites diferentes para escalar e reduzir horizontalmente com base em situações práticas.

Estamos *não é recomendável* configurações de dimensionamento automático como exemplos de saudação abaixo com hello valores de limite mesmo ou muito semelhantes para sair e entrar condições:

* Aumentar as instâncias por contagem de 1 quando a Contagem de Threads < = 600
* Reduzir as instâncias por contagem de 1 quando a Contagem de Threads >= 600

Vejamos um exemplo de como o que pode levar o comportamento de tooa que pode parecer confuso. Considere Olá sequência a seguir.

1. Suponha que há 2 toobegin instâncias com e, em seguida, o número médio de saudação de threads por instância cresce too625.
2. O dimensionamento automático escala horizontalmente uma terceira instância.
3. Em seguida, suponha que contagem de threads de média de saudação em instância fica too575.
4. Antes de redução, o dimensionamento automático tenta tooestimate estado final Olá será se ele é dimensionado em. Por exemplo, 575 x 3 (contagem de instância atual) = 1.725 / 2 (número final de instâncias quando reduzido verticalmente) = 862.5 threads. Isso significa AutoEscala teria tooimmediately expansão novamente mesmo depois que ele dimensionada, se Olá thread médio contagem permanece Olá mesmo ou até mesmo se apenas uma pequena quantidade. No entanto, se ele expandidos novamente, deve repetir o processo inteiro hello, resultando tooan infinita.
5. tooavoid nessa situação (chamada de "falta de sincronismo"), dimensionamento automático não expande para baixo em todos os. Em vez disso, ele ignora e reavalia Olá condição novamente trabalho Olá próximo tempo saudação do serviço é executado. Isso pode confundir muitas pessoas porque o dimensionamento automático não aparece toowork quando a contagem de threads de média de saudação foi 575.

Estimativa durante uma escala é pretendido tooavoid "oscilando" situações, em que ações em escala e expansão continuamente ir e voltar. Lembre-se esse comportamento quando você escolhe Olá mesmos limites de escalabilidade horizontal e no.

É recomendável escolher uma margem suficiente entre Olá expansão e em limites. Por exemplo, considere Olá melhor combinação de regra a seguir.

* Aumentar as instâncias por contagem de 1 quando CPU% >= 80
* Reduzir as instâncias por contagem de 1 quando CPU% <= 60

Nesse caso  

1. Suponha que há 2 toostart instâncias com.
2. Se Olá porcentagem média de CPU em instâncias ficar too80, dimensionamento automático seja dimensionável adicionando uma terceira instância.
3. Agora suponha pela hora Olá CPU % cai too60.
4. Regra na escala do dimensionamento automático calcula o estado final Olá se fosse tooscale-in. Por exemplo, 60 x 3 (contagem de instância atual) = 180 / 2 (número final de instâncias quando reduzido verticalmente) = 90 threads. Para dimensionamento automático não escala-in porque ela teria tooscale-out novamente imediatamente. Em vez disso, ele ignora a redução vertical.
5. Olá próximo tempo AutoEscala verifica, Olá CPU continua toofall too50. Estima novamente - instância 50 x 3 = 150 / 2 instâncias = 75, que está abaixo do limite de escalabilidade horizontal de saudação de 80, para que ele é dimensionado em instâncias de too2 com êxito.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Considerações sobre valores de dimensionamento de limite para métricas especiais
 Para métricas especiais, como a métrica do comprimento da fila do barramento de serviço ou de armazenamento, o limite de saudação é número médio de saudação de mensagens disponíveis por número atual de instâncias. Escolha cuidadosamente Olá escolha Olá valor de limite para esta métrica.

Vamos ilustrá-lo com um exemplo tooensure você entender o comportamento de saudação melhor.

* Aumentar o número de instâncias por contagem de 1 quando a contagem de mensagem de Fila de Armazenamento > = 50
* Reduzir o número de instâncias por contagem 1 de contagem de mensagem de Fila de Armazenamento > = 10

Considere Olá sequência a seguir:

1. Há duas instâncias de fila de armazenamento.
2. Mensagens continuam chegando e ao examinar a fila de armazenamento hello, contagem total de saudação lê 50. Você pode pressupor que o dimensionamento automático deve iniciar uma ação de escala horizontal. No entanto, observe que ainda é 50/2 = 25 mensagens por instância. Portanto, a escala horizontal não ocorrerá. Para Olá primeiro toohappen de expansão, contagem total de mensagens de saudação na fila de armazenamento Olá deve ser 100.
3. Em seguida, suponha que a contagem total de mensagens de saudação atinge 100.
4. Uma instância de fila de armazenamento 3º é adicionada devido a ação de expansão tooa.  Olá próxima ação de expansão não acontecerá até Olá total contagem de mensagens na fila de saudação atinge 150 pois 150/3 = 50.
5. Agora número Olá de mensagens na fila de saudação é reduzido. Com 3 instâncias, ação de escala no primeiro Olá acontece quando hello total de mensagens em todas as filas somar too30 porque 30/3 = 10 mensagens por instância, que é o limite de escala em hello.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Considerações sobre dimensionamento quando vários perfis são configurados em uma configuração de dimensionamento automático
Em uma configuração de dimensionamento automático, você pode escolher um perfil padrão, que é sempre aplicado sem qualquer dependência de agenda ou hora, ou você pode escolher um perfil recorrente ou um perfil para um período fixo com um intervalo de data e hora.

Quando o serviço de AutoEscala processa-las, sempre verifica no hello ordem a seguir:

1. Perfil de Data Fixa
2. Perfil recorrente
3. Perfil ("Sempre") Padrão

Se um perfil condição for atendida, dimensionamento automático não verifica a próxima condição de perfil Olá abaixo dela. O dimensionamento automático só processa um perfil por vez. Isso significa que, se você quiser tooalso incluem uma condição de processamento de um perfil de camada inferior, você deve incluir essas regras também no perfil atual hello.

Vamos examinar isso usando um exemplo:

imagem de saudação abaixo mostra uma configuração de AutoEscala com um perfil de padrão de instâncias mínimas = 2 e máximo de instâncias = 10. Neste exemplo, regras são configurada tooscale-out quando Olá a contagem de mensagens na fila de saudação é maior que 10 e na escala quando a contagem de mensagem de saudação na fila de saudação é menor que 3. Agora o recurso Olá pode dimensionar entre 2 e 10 instâncias.

Além disso, há um perfil recorrente para segunda-feira. Ele é definido para instâncias mínimas = 2 e máximo de instâncias = 12. Isso significa que na segunda-feira, Olá primeiro tempo AutoEscala procura por esta condição, se a contagem de instâncias de saudação for 2, ele é dimensionado toohello mínimo de 3. Como AutoEscala continua toofind essa condição de perfil correspondente (segunda-feira), ele processará somente Olá CPU regras baseadas em escala-out ou em configurado para este perfil. Neste momento, ele não verifica para comprimento da fila de saudação. No entanto, se você deseja comprimento de fila de saudação condição toobe marcada, você deve incluir essas regras de perfil de padrão de saudação bem em seu perfil de segunda-feira.

Da mesma forma, quando o dimensionamento automático muda toohello back padrão perfil, ele primeiro verifica se Olá mínimo e máximo condições. Se o número de saudação de instâncias em tempo de saudação for 12, ele é dimensionado em too10, Olá máximo permitido para o perfil de padrão de saudação.

![configurações de dimensionamento automático](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Considerações sobre dimensionamento quando várias regras são configuradas em um perfil
Há casos em que você pode ter tooset várias regras em um perfil. Olá conjunto de regras de AutoEscala a seguir é usado pelo uso de serviços quando várias regras são definidas.

Em *escalar horizontalmente*, o dimensionamento automático será executado se nenhuma regra for atendida.
Em *em escala*, AutoEscala exigem todas as regras toobe atendidos.

tooillustrate, suponha que você tenha Olá seguindo as regras de AutoEscala 4:

* Se CPU < 30%, reduza horizontalmente em 1
* Se Memória < 50%, reduza horizontalmente em 1
* Se CPU < 75%, escale horizontalmente em 1
* Se Memória < 75, escale horizontalmente em 1

Em seguida, siga Olá ocorre:

* Se a CPU for 76% e a Memória 50%, escalaremos horizontalmente.
* Se a CPU for 50% e a Memória 76%, escalaremos horizontalmente.

Olá por outro lado, se a CPU é 25% e memória faz AutoEscala 51% **não** na escala. Tooscale-in, CPU deve ser 29% e memória 49%.

### <a name="always-select-a-safe-default-instance-count"></a>Sempre selecione uma contagem de instância de segurança padrão
Contagem de instâncias padrão Olá é importante AutoEscala sua contagem de toothat de serviço é dimensionado quando métricas não estão disponíveis. Portanto, selecione uma contagem de instância padrão que seja segura para suas cargas de trabalho.

### <a name="configure-autoscale-notifications"></a>Configurar notificações de dimensionamento automático
Dimensionamento automático notifica administradores hello e colaboradores de recurso Olá por email se ocorrer qualquer uma das seguintes condições de saudação:

* serviço de dimensionamento automático não tootake uma ação.
* Métricas não estão disponíveis para o serviço de AutoEscala toomake uma decisão de escala.
* Métricas estão disponível (recuperação) toomake novamente uma decisão de escala.
  Além disso condições toohello acima, você pode configurar tooget de notificações por email ou webhook notificado para ações de dimensionamento bem-sucedido.
  
Você também pode usar uma integridade do Log de atividades toomonitor alerta saudação do mecanismo de dimensionamento automático hello. Aqui estão exemplos muito[criar um alerta de Log da atividade toomonitor todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) ou muito[criar um alerta de Log da atividade toomonitor todos Falha na escala de dimensionamento automático em / expansão de operações no sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Próximas etapas
- [Crie um alerta de Log da atividade toomonitor todas as operações de mecanismo de dimensionamento automático em sua assinatura.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Criar um alerta de Log da atividade toomonitor todos Falha na escala de dimensionamento automático em / expansão de operações em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
