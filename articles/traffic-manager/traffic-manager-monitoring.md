---
title: monitoramento do ponto de extremidade do Traffic Manager aaaAzure | Microsoft Docs
description: "Este artigo pode ajudá-lo a entender como o Traffic Manager usa o monitoramento de ponto de extremidade e toohelp de failover automático do ponto de extremidade do Azure clientes implantam aplicativos de alta disponibilidade"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Monitoramento de ponto de extremidade do Gerenciador de Tráfego

O Gerenciador de Tráfego do Azure inclui monitoramento de ponto de extremidade interno e failover automático de ponto de extremidade. Esse recurso ajuda a fornecer aplicativos de alta disponibilidade que são falha tooendpoint resiliente, inclusive falhas de região do Azure.

## <a name="configure-endpoint-monitoring"></a>Configurar o monitoramento de pontos de extremidade

monitoramento de ponto de extremidade tooconfigure, você deve especificar Olá configurações a seguir em seu perfil do Gerenciador de tráfego:

* **Protocolo**. Escolha HTTP, HTTPS ou TCP como protocolo de saudação do Traffic Manager usa quando probing toocheck seu ponto de extremidade sua integridade. O monitoramento HTTPS não verifica se o certificado SSL é válido - ele verifica apenas esse Olá certificado está presente.
* **Porta**. Escolha Olá porta usada para a solicitação de saudação.
* **Caminho**. Esta configuração é válida somente para Olá protocolos HTTP e HTTPS, para o qual configuração de caminho de saudação especificando é necessária. Fornecendo essa configuração para Olá TCP monitoramento protocolo resulta em erro. Para o protocolo TCP, forneça caminho relativo da saudação e nome de saudação do Olá página da Web ou arquivo hello que Olá acessos de monitoramento. Uma barra invertida (/) é uma entrada válida para o caminho relativo da saudação. Esse valor indica que se o arquivo hello está no diretório raiz de saudação (padrão).
* **Intervalo de investigação**. Esse valor especifica a frequência com que a integridade de um ponto de extremidade é verificada usando um agente de investigação do Gerenciador de Tráfego. Você pode especificar dois valores aqui: 30 segundos (investigação normal) e 10 segundos (investigação rápida). Se nenhum valor for fornecido, o perfil de saudação define tooa valor de padrão de 30 segundos. Visite Olá [preços do Gerenciador de tráfego](https://azure.microsoft.com/pricing/details/traffic-manager) página toolearn mais sobre preços de probing rápida.
* **Número de falhas tolerado**. Esse valor especifica quantas falhas um agente de investigação do Gerenciador de Tráfego tolera antes de marcar o ponto de extremidade como não íntegro. Seu valor pode variar entre 0 e 9. Um valor 0 significa que uma única falha de monitoramento pode causar esse toobe de ponto de extremidade marcado como não íntegro. Se nenhum valor for especificado, ele usa o valor padrão de saudação de 3.
* **Tempo limite de monitoramento**. Essa propriedade especifica a quantidade de saudação de saudação do tempo do Traffic Manager agent probing deve aguardar antes de considerar que verificam a uma falha quando um teste de verificação de integridade é enviado toohello de ponto de extremidade. Se Olá que intervalo de sondagem é definido too30 segundos, em seguida, você pode definir o valor de tempo limite de saudação entre 5 e 10 segundos. Se nenhum valor for especificado, ele usará um valor padrão de 10 segundos. Se Olá que intervalo de sondagem é definido too10 segundos, em seguida, você pode definir o valor de tempo limite de saudação entre 5 e 9 segundos. Se nenhum valor de Tempo Limite for especificado, ele usará um valor padrão de 9 segundos.

![Monitoramento de ponto de extremidade do Gerenciador de Tráfego](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Figura 1: Monitoramento de ponto de extremidade do Gerenciador de Tráfego**

## <a name="how-endpoint-monitoring-works"></a>Como o monitoramento de ponto de extremidade funciona

Se Olá monitoramento protocolo é definido como HTTP ou HTTPS, agente probing do hello Traffic Manager faz um GET solicitação toohello ponto de extremidade usando o protocolo de saudação, porta e caminho relativo fornecido. Se ele obtiver de volta uma resposta 200-OK, esse ponto de extremidade será considerado íntegro. Se a resposta de saudação é um valor diferente, ou se nenhuma resposta for recebida dentro do período de tempo limite de saudação especificado, hello sondando o agente do Traffic Manager tentará novamente configuração tolerado, número de falhas de toohello (não tentará novamente terminar se essa configuração for 0) de acordo com . Se várias falhas consecutivas Olá for maior do que a configuração de tolerado, número de falhas de saudação, esse ponto de extremidade está marcado como não íntegro. 

Se Olá monitoramento protocolo for TCP, o agente de probing de Gerenciador de tráfego de Olá inicia uma solicitação de conexão TCP usando a porta de saudação especificada. Se o ponto de extremidade Olá responde solicitação toohello com uma conexão de saudação do resposta tooestablish, que a verificação de integridade está marcada como um êxito e agente probing do Gerenciador de tráfego Olá redefine a conexão de TCP hello. Se a resposta de saudação é um valor diferente, ou se nenhuma resposta for recebida dentro de período de tempo limite de saudação especificado, Olá sondando o agente do Traffic Manager tentará novamente a configuração de tolerado, número de falhas de toohello (nenhum novamente são feitas tentativas de se essa configuração for 0) de acordo com. Se várias falhas consecutivas Olá for maior do que a configuração de tolerado, número de falhas de saudação, esse ponto de extremidade é marcado não íntegro.

Em todos os casos, o Traffic Manager sondas de vários locais e determinação de falhas consecutivas Olá acontece dentro de cada região. Isso também significa que os pontos de extremidade estão recebendo investigações de integridade do Gerenciador de tráfego com uma frequência superior configuração Olá usada para o intervalo de sondagem.

>[!NOTE]
>Para HTTP ou HTTPS de protocolo de monitoramento, uma prática comum no lado do ponto de extremidade de saudação é tooimplement uma página personalizada dentro de seu aplicativo - por exemplo, /health.aspx. Usando esse caminho para monitoramento, você pode executar verificações específicas do aplicativo, como verificação de contadores de desempenho ou da disponibilidade do banco de dados. Página de saudação com base nessas verificações personalizadas, retorna um código de status HTTP apropriado.

Todos os pontos de extremidade em um perfil do Gerenciador de Tráfego compartilham configurações de monitoramento. Se você precisar toouse diferentes configurações de monitoramento para diferentes pontos de extremidade, você pode criar [aninhados perfis do Traffic Manager](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Status do ponto de extremidade e do perfil

Você pode habilitar e desabilitar pontos de extremidade e perfis do Gerenciador de Tráfego. No entanto, uma alteração no status do ponto de extremidade também pode ocorrer como resultado das configurações e processos automatizados do Gerenciador de Tráfego.

### <a name="endpoint-status"></a>Status do ponto de extremidade

Você pode habilitar ou desabilitar um ponto de extremidade específico. serviço subjacente Hello, que pode ainda ser íntegro, não é afetado. Controles alteração de status de ponto de extremidade Olá Olá disponibilidade do ponto de extremidade de Olá Olá perfil do Traffic Manager. Quando um status de ponto de extremidade estiver desabilitado, Gerenciador de tráfego não verifica sua integridade e ponto de extremidade de saudação não está incluído em uma resposta DNS.

### <a name="profile-status"></a>Status do perfil

Usando a configuração de status de perfil hello, você pode habilitar ou desabilitar um perfil específico. Enquanto o status do ponto de extremidade afeta um único ponto de extremidade, o status do perfil afeta todo perfil hello, incluindo todos os pontos de extremidade. Quando você desabilita um perfil, pontos de extremidade de saudação não são verificados quanto à integridade e nenhum ponto de extremidade está incluídos em uma resposta DNS. Um [NXDOMAIN](https://tools.ietf.org/html/rfc2308) código de resposta é retornado para consultas DNS hello.

### <a name="endpoint-monitor-status"></a>Status do monitor de ponto de extremidade

Monitora o status de ponto de extremidade é um valor gerado pelo Gerenciador de tráfego que mostra o status de saudação do ponto de extremidade de saudação. Você não pode alterar essa configuração manualmente. status do monitor de ponto de extremidade de saudação é uma combinação dos resultados de saudação do monitoramento de ponto de extremidade e Olá status do ponto de extremidade configurado. os valores possíveis de saudação do status do monitor de ponto de extremidade são mostrados na Olá a tabela a seguir:

| Status do perfil | Status do ponto de extremidade | Status do monitor de ponto de extremidade | Observações |
| --- | --- | --- | --- |
| Desabilitado |Habilitado |Inativo |perfil de saudação foi desabilitado. Embora o status do ponto de extremidade Olá estiver habilitado, o status do perfil hello (desabilitado) terá precedência. Pontos de extremidade em perfis desabilitados não são monitorados. Um código de resposta NXDOMAIN é retornado para a consulta DNS hello. |
| &lt;qualquer&gt; |Desabilitado |Desabilitado |ponto de extremidade de saudação foi desabilitado. Pontos de extremidade desabilitados não são monitorados. ponto de extremidade de saudação não está incluído em respostas DNS, portanto, ele não receber tráfego. |
| habilitado |Habilitado |Online |ponto de extremidade de saudação é monitorado e está íntegro. Ele é incluído em respostas DNS e pode receber tráfego. |
| Habilitado |Habilitado |Degradado |As verificações de integridade de monitoramento do ponto de extremidade estão falhando. ponto de extremidade de saudação não está incluído em respostas DNS e não recebe o tráfego. <br>Toothis uma exceção é se todos os pontos de extremidade são degradados, caso em que todos eles são considerados toobe retornado na resposta de consulta de saudação).</br>|
| habilitado |Habilitado |Verificando ponto de extremidade |ponto de extremidade Olá será monitorado, mas os resultados de saudação da saudação primeira investigação ainda não foram recebidos. Verificando ponto de extremidade é um estado temporário que geralmente ocorre imediatamente após a adição ou habilitar um ponto de extremidade no perfil de saudação. Um ponto de extremidade nesse estado é incluído em respostas DNS e pode receber tráfego. |
| Habilitado |Habilitado |Parada |Olá nuvem serviço ou aplicativo web que Olá toois de pontos de extremidade não está em execução. Verifique as configurações do aplicativo hello nuvem web ou serviço. Isso também pode ocorrer se o ponto de extremidade de saudação é do tipo aninhado de ponto de extremidade e perfil de filho hello está desabilitado ou está inativo. <br>Um ponto de extremidade com um status Parado não é monitorado. Ele não é incluído em respostas DNS e não recebe tráfego. Toothis uma exceção é se todos os pontos de extremidade são degradados, caso em que todos eles serão considerados toobe retornado na resposta de consulta de saudação.</br>|

Para obter detalhes sobre como o status do monitor de ponto de extremidade é calculado para pontos de extremidade aninhados, veja [Perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Status do monitor de perfil

status do monitor de perfil de saudação é uma combinação de valores de status de monitor de ponto de extremidade de Olá para todos os pontos de extremidade e de status do perfil de saudação configurado. Olá possíveis valores são descritos em Olá a tabela a seguir:

| Status do perfil (conforme configurado) | Status do monitor de ponto de extremidade | Status do monitor de perfil | Observações |
| --- | --- | --- | --- |
| Desabilitado |&lt;qualquer&gt; ou um perfil sem pontos de extremidade definidos. |Desabilitado |perfil de saudação foi desabilitado. |
| habilitado |status de saudação de pelo menos um ponto de extremidade está degradado. |Degradado |Examine o status de cada ponto de extremidade de Olá valores toodetermine quais pontos de extremidade exigem atenção adicional. |
| habilitado |status de saudação de pelo menos um ponto de extremidade está Online. Nenhum ponto de extremidade tem o status Degradado. |Online |serviço de saudação está aceitando o tráfego. Nenhuma ação adicional é necessária. |
| habilitado |status de saudação de pelo menos um ponto de extremidade está verificando ponto de extremidade. Nenhum ponto de extremidade tem status Online ou Degradado. |Verificando pontos de extremidade |Esse estado de transição ocorre quando um perfil é criado ou habilitado. integridade do ponto de extremidade Hello está sendo verificada para Olá primeira vez. |
| habilitado |status de saudação de todos os pontos de extremidade no perfil de saudação são desativados ou interrompidos ou perfil de saudação não tem nenhum ponto de extremidade definido. |Inativo |Nenhum ponto de extremidade está ativo, mas Olá perfil ainda está habilitado. |

## <a name="endpoint-failover-and-recovery"></a>Failover e recuperação do ponto de extremidade

Gerenciador de tráfego periodicamente verifica a integridade de saudação de cada ponto de extremidade, incluindo pontos de extremidade não íntegro. O Gerenciador de Tráfego detecta quando um ponto de extremidade se torna íntegro e coloca-o de volta em rotação.

Um ponto de extremidade não está íntegro quando qualquer Olá eventos a seguir ocorrer:
- Se Olá monitoramento protocolo HTTP ou HTTPS:
    - Uma resposta diferente de 200 será recebida (incluindo um código 2xx diferente ou um redirecionamento 301/302).
- Se Olá monitoramento protocolo for TCP: 
    - Uma resposta diferente de ACK ou SYN ACK é recebido na solicitação de sincronização de toohello de resposta enviada pelo Gerenciador de tráfego tooattempt um estabelecimento de conexão.
- Tempo limite. 
- Qualquer outro conexão problema resultante no ponto de extremidade de saudação que não estão acessíveis.

Para obter mais informações sobre como solucionar problemas de verificações com falha, consulte [Solução de problemas de status degradado no Gerenciador de Tráfego do Azure](traffic-manager-troubleshooting-degraded.md). 

Olá, linha do tempo abaixo na Figura 2 é uma descrição detalhada da saudação monitorando o processo de ponto de extremidade do Gerenciador de tráfego que tem Olá configurações a seguir: monitoramento protocolo é HTTP, o intervalo de sondagem é de 30 segundos, o número de falhas toleradas é 3, o valor de tempo limite é de 10 segundos e TTL do DNS é de 30 segundos.

![Sequência de failover e failback de ponto de extremidade do Gerenciador de Tráfego](./media/traffic-manager-monitoring/timeline.png)

**Figura 2: Failover do ponto de extremidade do Gerenciador de Tráfego e sequência de recuperação**

1. **GET**. Para cada ponto de extremidade, Olá sistema de monitoramento do Traffic Manager executa uma solicitação GET no caminho de saudação especificado no hello configurações de monitoramento.
2. **200 OK**. saudação de sistema de monitoramento espera uma toobe de mensagem HTTP 200 Okey retornada dentro de 10 segundos. Quando ele recebe essa resposta, ele reconhecerá que Olá serviço está disponível.
3. **30 segundos entre verificações**. verificação de integridade do ponto de extremidade de saudação é repetida a cada 30 segundos.
4. **Serviço indisponível**. serviço de saudação se torna indisponível. Gerenciador de tráfego não saberá até a próxima verificação de integridade hello.
5. **Saudação de tooaccess tentativas monitoramento caminho**. saudação de sistema de monitoramento executa uma solicitação GET, mas não receber uma resposta no período de tempo limite de saudação de 10 segundos (como alternativa, uma resposta 200 não pode ser recebida). Posteriormente, ele realiza mais três tentativas em intervalos de 30 segundos. Se uma das tentativas de saudação for bem-sucedida, número de saudação de tentativas será redefinido.
6. **Status definido tooDegraded**. Após a quarta falha consecutiva, Olá sistema de monitoramento marca status do ponto de extremidade disponível hello como degradado.
7. **O tráfego é pontos de extremidade desviadas tooother**. Olá servidores de nome DNS do Traffic Manager são atualizados e Gerenciador de tráfego não retorna o ponto de extremidade de saudação em consultas de tooDNS de resposta. Novas conexões são tooother direcionado, pontos de extremidade disponíveis. No entanto, respostas DNS anteriores que incluem esse ponto de extremidade ainda poderão ser armazenadas em cache por servidores DNS recursivos e clientes DNS. Os clientes continuam o ponto de extremidade do toouse Olá até expira Olá cache DNS. Como Olá cache DNS expira, os clientes fazem novas consultas DNS e toodifferent direcionado de pontos de extremidade. duração do cache de saudação é controlada pela configuração de TTL Olá no hello perfil do Traffic Manager, por exemplo, de 30 segundos.
8. **Continuação das verificações de integridade**. O Traffic Manager continuará toocheck integridade de saudação do ponto de extremidade de saudação enquanto ele tem um status degradado. O Traffic Manager detecta quando o ponto de extremidade de saudação retorna toohealth.
9. **Serviço volta a ficar online**. serviço de saudação se torna disponível. ponto de extremidade Olá retém seu status de degradado no Traffic Manager até que o sistema de monitoramento de saudação executa sua próxima verificação de integridade.
10. **Tráfego tooservice retoma**. O Gerenciador de Tráfego envia uma solicitação GET e recebe uma resposta de status 200 OK. serviço de saudação retornou tooa o estado íntegro. servidores de nome do Gerenciador de tráfego de saudação são atualizados e iniciar toohand nome de DNS do serviço de saudação em respostas DNS. Tráfego retorna toohello de ponto de extremidade como expirarem em cache as respostas DNS que retornam outros pontos de extremidade e como as conexões existentes são encerrados tooother pontos de extremidade.

    > [!NOTE]
    > Como o Traffic Manager funciona no nível DNS de saudação, ele não pode influenciar o ponto de extremidade de tooany conexões existentes. Quando ele direciona o tráfego entre os pontos de extremidade (ou pelas configurações de perfil alterados ou durante o failover ou failback), o Traffic Manager direciona novos pontos de extremidade de tooavailable de conexões. No entanto, outros pontos de extremidade podem continuar tooreceive tráfego por meio de conexões existentes até que as sessões são encerradas. aplicativos do tooenable toodrain de tráfego de conexões existentes, devem limitar Olá usada com cada ponto de extremidade de duração da sessão.

## <a name="traffic-routing-methods"></a>Métodos de roteamento de tráfego

Quando um ponto de extremidade tem um status degradado, ele não é retornado em consultas de tooDNS de resposta. Em vez disso, um ponto de extremidade alternativo será escolhido e retornado. o método de roteamento de tráfego de saudação configurado no perfil de saudação determina como o ponto de extremidade alternativo Olá é escolhido.

* **Prioridade**. Os pontos de extremidade formam uma lista priorizada. Olá primeiro ponto de extremidade disponível na lista de saudação sempre é retornado. Se um status de ponto de extremidade está degradado, Olá próximo disponível ponto de extremidade é retornado.
* **Ponderado**. Qualquer ponto de extremidade disponível é escolhido aleatoriamente com base em seus pesos atribuídos e Olá pesos de saudação outros pontos de extremidade disponíveis.
* **Desempenho**. Olá ponto de extremidade mais próximo usuário final toohello é retornado. Se esse ponto de extremidade não estiver disponível, um ponto de extremidade é escolhido aleatoriamente de Olá a todos os outros pontos de extremidade disponíveis. Escolher um ponto de extremidade aleatório evita uma falha em cascata que pode ocorrer quando o ponto de extremidade mais próximo Avançar Olá fica sobrecarregado. Você pode configurar planos de failover alternativos para o roteamento de tráfego de desempenho usando [perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Geográfico**. ponto de extremidade de saudação mapeado tooserve Olá geográfica com base na solicitação de consulta de saudação que IP será retornado. Se esse ponto de extremidade não estiver disponível, outro ponto de extremidade não será toofailover selecionado, como uma localização geográfica pode ser mapeado somente tooone ponto de extremidade em um perfil (mais detalhes estão na Olá [perguntas frequentes sobre](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Como prática recomendada, ao usar o roteamento geográfico, é recomendável clientes perfis do Gerenciador de tráfego toouse aninhado com mais de um ponto de extremidade como pontos de extremidade de saudação do perfil de saudação.

Para obter mais informações, consulte [Métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md).

> [!NOTE]
> Uma exceção toonormal roteamento de tráfego ocorre quando todos os pontos de extremidade qualificados têm um estado degradado. O Traffic Manager faz a tentativa de "melhor esforço" e *responde como se todos os pontos de status degradado Olá realmente estão no estado online*. Esse comportamento é preferível toohello alternativa, que seria toonot retornar qualquer ponto de extremidade em Olá resposta DNS. Pontos de extremidade com status Parado ou Desabilitado não são monitorados e, portanto, não são considerados qualificados para o tráfego.
>
> Essa condição geralmente é causada pela configuração incorreta do serviço Olá, como:
>
> * Verifica uma lista de controle de acesso (ACL) bloqueando a integridade do Gerenciador de tráfego de saudação.
> * Uma configuração incorreta de monitoramento de porta ou protocolo no perfil do Gerenciador de tráfego de saudação do hello.
>
> Olá consequência desse comportamento é que, se as verificações de integridade do Traffic Manager não estiverem configuradas corretamente, talvez pareça tráfego hello como se o roteamento do Traffic Manager *é* funcionando corretamente. No entanto, neste caso, o failover do ponto de extremidade não acontece e isso afeta a disponibilidade geral do aplicativo. É importante toocheck perfil Olá mostra um status Online, não um status degradado. Um status Online indica que Olá Traffic Manager verificações de integridade estão funcionando como esperado.

Para obter mais informações sobre como solucionar problemas de verificações de integridade com falha, consulte [Solução de problemas de status Degradado no Gerenciador de Tráfego do Azure](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Próximas etapas

Saiba [como funciona o Gerenciador de Tráfego](traffic-manager-how-traffic-manager-works.md)

Saiba mais sobre Olá [métodos de roteamento de tráfego](traffic-manager-routing-methods.md) suportada pelo Gerenciador de tráfego

Saiba como muito[criar um perfil do Gerenciador de tráfego](traffic-manager-manage-profiles.md)

[Solucionar problemas de status Degradado](traffic-manager-troubleshooting-degraded.md) em um ponto de extremidade do Gerenciador de Tráfego
