---
title: "métodos de roteamento de tráfego aaaAzure Traffic Manager - | Microsoft Docs"
description: "Isso ajuda a que entender os métodos de roteamento de tráfego diferente do hello usados pelo Gerenciador de tráfego de artigos"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Métodos de roteamento do Gerenciador de Tráfego

Azure Traffic Manager oferece suporte a quatro roteamento de tráfego métodos toodetermine como tooroute rede tráfego toohello vários pontos de extremidade de serviço. Gerenciador de tráfego se aplica a saudação roteamento de tráfego método tooeach consulta DNS recebe. método de roteamento de tráfego Hello determina qual ponto de extremidade retornado na resposta do DNS hello.

Quatro métodos de roteamento de tráfego estão disponíveis no Gerenciador de Tráfego:

* **[Prioridade](#priority):** selecione **prioridade** quando você deseja toouse um ponto de extremidade de serviço primário para todo o tráfego e fornecer backups caso Olá primário ou pontos de extremidade de backup Olá estão indisponíveis.
* **[Ponderado](#weighted):** selecione **ponderado** quando você quiser toodistribute tráfego em um conjunto de pontos de extremidade, ou uniformemente ou tooweights acordo, que você definir.
* **[Desempenho](#performance):** selecione **desempenho** quando tiver pontos de extremidade em diferentes locais geográficos e desejar que os usuários finais toouse hello "mais próximo" ponto de extremidade em termos da menor latência de rede hello.
* **[Geográfico](#geographic):** selecione **geográfica** para que os usuários toospecific direcionado pontos de extremidade (do Azure, externa ou aninhadas) com base em qual localização geográfica sua consulta DNS se origina. Isso permite cenários de tooenable de clientes do Traffic Manager onde saber região geográfica do usuário e roteá-los com base no que são importante. Os exemplos incluem conformidade com normas de soberania de dados, localização de conteúdo e experiência do usuário, bem como medição do tráfego de diferentes regiões.

Todos os perfis do Gerenciador de Tráfego incluem o monitoramento da integridade do ponto de extremidade e o failover automático do ponto de extremidade. Para obter mais informações, consulte [Monitoramento do Ponto de Extremidade do Gerenciador de Tráfego](traffic-manager-monitoring.md). Um único perfil do Gerenciador de Tráfego pode usar apenas um único método de roteamento de tráfego. Você pode selecionar um método de roteamento de tráfego diferente para o seu perfil a qualquer momento. As alterações são aplicadas em até um minuto e não há tempo de inatividade. Métodos de roteamento de tráfego podem ser combinados usando perfis aninhados do Gerenciador de Tráfego. O aninhamento permite sofisticadas e flexíveis configurações de roteamento de tráfego que atendam às necessidades de saudação de maiores aplicativos complexos. Para obter mais informações, consulte [perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).

## <a name = "priority"></a>Método de roteamento de tráfego por prioridade

Geralmente uma organização deseja tooprovide confiabilidade de seus serviços Implantando um ou mais serviços de backup no caso do serviço primário fica. método Hello roteamento de tráfego 'Priority' permite que o Azure clientes tooeasily implementar esse padrão de failover.

![Método de roteamento de tráfego por “Prioridade” do Gerenciador de Tráfego do Azure][1]

Olá perfil do Traffic Manager contém uma lista priorizada de pontos de extremidade de serviço. Por padrão, o Traffic Manager envia todos os tráfego toohello (prioridade mais alta-) ponto de extremidade primário. Se o ponto de extremidade Olá primário não estiver disponível, o Gerenciador de tráfego rotas Olá segundo ponto de extremidade do tráfego toohello. Se ambos os pontos de extremidade primário e secundário Olá não estiverem disponíveis, o tráfego de saudação vai toohello em terceiro lugar, e assim por diante. Disponibilidade do ponto de extremidade de saudação é com base no status de saudação configurada (habilitado ou desabilitado) e Olá monitoramento de ponto de extremidade em andamento.

### <a name="configuring-endpoints"></a>Configurando pontos de extremidade

No Gerenciador de recursos do Azure, você configurar a prioridade de ponto de extremidade Olá explicitamente usando a propriedade de 'priority' hello para cada ponto de extremidade. Essa propriedade é um valor entre 1 e 1000. Valores mais baixos representam uma prioridade mais alta. Pontos de extremidade não podem compartilhar os valores de prioridade. Definir propriedade de saudação é opcional. Quando omitido, uma prioridade padrão com base na ordem de ponto de extremidade de saudação é usada.

##<a name = "weighted"></a>Método de roteamento de tráfego ponderado
método Hello roteamento de tráfego 'Ponderado' permite tráfego toodistribute uniformemente ou toouse uma ponderação predefinida.

![Método de roteamento de tráfego “Ponderado” do Gerenciador de Tráfego do Azure][2]

Método roteamento de tráfego ponderada de hello, você atribuir um ponto de extremidade de tooeach peso na configuração do perfil do Traffic Manager hello. peso de saudação é um inteiro de 1 too1000. Esse parâmetro é opcional. Se ele for omitido, os Gerenciadores de Tráfego usarão um peso padrão de “1”.

Para cada consulta DNS recebida, o Gerenciador de Tráfego escolhe aleatoriamente um ponto de extremidade disponível. probabilidade de saudação de escolher um ponto de extremidade baseia-se em Olá pesos atribuídos tooall pontos de extremidade disponíveis. Mesmo usando Olá peso em todos os resultados de pontos de extremidade em um mesmo a distribuição de tráfego. Usando pesos superior ou inferiores em pontos de extremidade específicos faz com que esses toobe de pontos de extremidade mais ou menos frequente retornados em respostas DNS de saudação.

método Hello ponderada permite que alguns cenários úteis:

* Atualização gradual do aplicativo: alocar uma percentagem do tráfego tooroute tooa novo ponto de extremidade e aumentar gradualmente o tráfego de Olá % too100 de tempo.
* TooAzure de migração do aplicativo: criar um perfil com pontos de extremidade do Azure e externos. Ajuste o peso de saudação do hello pontos de extremidade tooprefer Olá novos pontos de extremidade.
* Intermitência de nuvem para capacidade adicional: expandir rapidamente uma implantação de local para nuvem hello, colocando atrás de um perfil do Gerenciador de tráfego. Quando precisar de capacidade extra na nuvem Olá, você pode adicionar ou permitir mais pontos de extremidade e especificar qual parte do tráfego vai tooeach de ponto de extremidade.

Olá portal do Gerenciador de recursos do Azure dá suporte à configuração de saudação do roteamento de tráfego ponderado.  Você pode configurar pesos usando versões do Gerenciador de recursos de saudação do Azure PowerShell, CLI e Olá APIs REST.

É importante toounderstand que as respostas DNS são armazenados em cache por clientes em por Olá recursiva os servidores DNS que Olá clientes usam os nomes DNS tooresolve. Esse cache pode ter um impacto nas distribuições de tráfego ponderado. Quando o número de saudação de clientes e servidores DNS recursivo é grande, a distribuição de tráfego funciona conforme o esperado. No entanto, quando o número de saudação de clientes ou servidores DNS recursivo é pequeno, o cache pode afetar significativamente a distribuição de tráfego hello.

Os casos de uso comuns incluem:

* Ambientes de desenvolvimento e teste
* Comunicações de aplicativo para aplicativo
* Aplicativos voltados para uma base de usuários estreita que compartilha uma infraestrutura comum de DNS recursivo (por exemplo, funcionários de uma empresa que se conectam por meio de um proxy)

Esses efeitos de cache DNS são comuns tooall tráfego com base em DNS roteamento sistemas, não apenas o Azure Traffic Manager. Em alguns casos, limpar explicitamente Olá cache DNS pode fornecer uma solução alternativa. Em outros casos, um método alternativo de roteamento de tráfego pode ser mais apropriado.

## <a name = "performance"></a>Método de roteamento de tráfego por desempenho

Implantar os pontos de extremidade em dois ou mais locais globo Olá pode melhorar a capacidade de resposta de saudação de muitos aplicativos pelo roteamento tráfego toohello local tooyou 'mais próximo'. Olá método de roteamento de tráfego 'Desempenho' fornece essa funcionalidade.

![Método de roteamento de tráfego por “Desempenho” do Gerenciador de Tráfego do Azure][3]

ponto de extremidade 'mais próximo' Hello não é necessariamente mais próximo, conforme medido pela distância geográfica. Em vez disso, Olá método de roteamento de tráfego 'Desempenho' determina o ponto de extremidade mais próximo Olá medindo a latência de rede. Gerenciador de tráfego mantém um tempo tabela de latência de Internet tootrack Olá ida e volta entre os intervalos de endereços IP e cada data center do Azure.

Gerenciador de tráfego procura Olá endereço IP de origem da solicitação DNS entrada hello na tabela de latência de Internet de saudação. Gerenciador de tráfego escolhe um ponto de extremidade disponível no hello datacenter do Azure que tem a menor latência Olá para esse intervalo de endereço IP e retorna o ponto de extremidade em Olá resposta DNS.

Como explicamos em [Como funciona o Gerenciador de Tráfego](traffic-manager-overview.md#how-traffic-manager-works), o Gerenciador de Tráfego não recebe consultas DNS diretamente de clientes. Em vez disso, as consultas DNS provenientes de serviço DNS recursivo Olá clientes Olá são toouse configurado. Portanto, hello endereço usado toodetermine Olá 'mais próximo' ponto de extremidade IP não é endereço IP saudação do cliente, mas ele é o endereço IP de saudação do serviço DNS recursivo hello. Na prática, esse endereço IP é um proxy válido para cliente hello.


Gerenciador de tráfego regularmente atualizações Olá tooaccount da tabela de latência de Internet para alterações em Olá Internet global e novas regiões do Azure. No entanto, desempenho do aplicativo varia de acordo com variações em tempo real de carga entre Olá da Internet. O roteamento de tráfego por desempenho não monitora a carga em um ponto de extremidade de serviço específico. No entanto, se um ponto de extremidade ficar indisponível, o Gerenciador de Tráfego não incluirá isso nas respostas a consultas DNS.


Toonote pontos:

* Se seu perfil contiver vários pontos de extremidade no hello mesma região do Azure, em seguida, o Traffic Manager distribui o tráfego igualmente entre pontos de extremidade disponíveis nessa região hello. Se preferir uma distribuição de tráfego diferente em uma região, use os [perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).
* Se todos habilitados os pontos de extremidade mais próximo de saudação região do Azure está degradado, Gerenciador de tráfego move pontos de extremidade do tráfego toohello na próxima região do Azure mais próximo hello. Se você quiser toodefine uma sequência de failover preferencial, use [aninhados perfis do Traffic Manager](traffic-manager-nested-profiles.md).
* Ao usar o método de roteamento de tráfego Olá desempenho com pontos de extremidade externos ou pontos de extremidade aninhados, você precisa toospecify localização Olá desses pontos. Escolha a implantação de tooyour mais próxima do hello região do Azure. Esses locais são valores de Olá Olá tabela de latência de Internet com suporte.
* algoritmo de saudação que escolhe o ponto de extremidade de saudação é determinístico. Repetido consultas DNS de saudação mesmo cliente é direcionados toohello mesmo ponto de extremidade. Normalmente, os clientes usam servidores DNS recursivo diferentes quando estão viajando. cliente Olá pode ser roteado tooa de ponto de extremidade diferente. Roteamento também pode ser afetado por atualizações toohello tabela de latência de Internet. Portanto, Olá desempenho método de roteamento de tráfego não garante que um cliente sempre é roteada toohello mesmo ponto de extremidade.
* Quando altera Olá tabela de latência de Internet, você pode perceber que alguns clientes são direcionados tooa de ponto de extremidade diferente. Essa alteração de roteamento é mais precisa com base nos dados de latência atuais. Essas atualizações são essenciais toomaintain precisão de saudação de desempenho como Olá que Internet continuamente evolui-roteamento de tráfego.

## <a name = "geographic"></a>Método de roteamento de tráfego geográfico

Perfis do Traffic Manager podem ser configurado toouse Olá geográfico método de roteamento para que os usuários são direcionados a pontos de extremidade toospecific (do Azure ou externas aninhadas) com base em qual localização geográfica, sua consulta DNS se origina de. Isso permite cenários de tooenable de clientes do Traffic Manager onde saber região geográfica do usuário e roteá-los com base no que são importante. Os exemplos incluem conformidade com normas de soberania de dados, localização de conteúdo e experiência do usuário, bem como medição do tráfego de diferentes regiões.
Quando um perfil é configurado para roteamento geográfico, cada ponto de extremidade associado perfil precisa toohave um conjunto de regiões geográficas atribuídos tooit. Uma região geográfica pode estar nos seguintes níveis de granularidade 
- Mundo – qualquer região
- Agrupamento Regional – por exemplo, África, Oriente Médio, Austrália/Pacífico etc. 
- País/região – por exemplo, Irlanda, Peru, RAE de Hong Kong etc. 
- Estado/Província – por exemplo, EUA-Califórnia, Austrália-Queensland, Canadá-Alberta etc. (observação: esse nível de granularidade conta com suporte apenas em Estados/províncias da Austrália, do Canadá, do Reino Unido e dos EUA).

Quando uma região ou um conjunto de regiões é atribuído o ponto de extremidade tooan, todas as solicitações dessas regiões obtém toothat somente roteado de ponto de extremidade. O Traffic Manager usa o endereço IP de origem Olá Olá DNS consulta toodetermine Olá da região do qual um usuário está consultando de – geralmente esse é o endereço IP de saudação do resolvedor DNS local Olá fazendo consulta Olá em nome de usuário de saudação.  

![Método de roteamento de tráfego "Geográfico" do Gerenciador de Tráfego do Azure](./media/traffic-manager-routing-methods/geographic.png)

O Traffic Manager lê o endereço IP de origem da saudação de consulta DNS hello e decide qual região geográfica se origina. Em seguida, parece toosee se houver um ponto de extremidade que tem este tooit região geográfica mapeado. Essa pesquisa começa no nível de granularidade mais baixo de saudação (estado/província onde ele é suportado, ou no nível de país/região Olá) e vai todos Olá um nível mais alto toohello, que é **World**. primeira correspondência de saudação encontrada usar essa passagem é designado como Olá tooreturn de ponto de extremidade na resposta de consulta de saudação. Quando houver correspondência com um ponto de extremidade do tipo Aninhado, um ponto de extremidade nesse perfil filho será retornado, com base em seu método de roteamento. Olá pontos a seguir é aplicáveis toothis comportamento:

- Uma região geográfica pode ser mapeado somente tooone ponto de extremidade em um perfil do Gerenciador de tráfego quando o tipo de roteamento Olá geográfica roteamento. Isso garante que o roteamento dos usuários seja determinístico e que os clientes possam habilitar cenários que exijam limites geográficos inequívocos.
- Se a região do usuário trata mapeamento geográfico em duas empresas diferentes, o Traffic Manager seleciona o ponto de extremidade de saudação com granularidade menor hello e não considera rotear solicitações de toohello essa região outro ponto de extremidade. Por exemplo, considere um perfil de tipo de Roteamento Geográfico com dois pontos de extremidade: Ponto de Extremidade 1 e Ponto de Extremidade 2. Endpoint1 está configurado tooreceive tráfego da Irlanda e Endpoint2 está configurado tooreceive tráfego na Europa. Se uma solicitação se origina da Irlanda, é sempre tooEndpoint1 roteadas.
- Como uma região pode ser mapeado somente de ponto de extremidade de tooone, o Traffic Manager retorna independentemente se o ponto de extremidade hello está íntegro ou não.

    >[!IMPORTANT]
    >É altamente recomendável que os clientes que usam o método de roteamento geográfico hello associá-lo com pontos de extremidade do hello aninhadas tipo que tem perfis filho que contém pelo menos dois pontos de extremidade dentro de cada.
- Se for encontrada uma correspondência de ponto de extremidade e esse ponto de extremidade é Olá **parado** estado, o Traffic Manager retorna uma resposta NODATA. Nesse caso, nenhum pesquisas adicionais é feita mais acima na hierarquia de região geográfica hello. Esse comportamento também é aplicável para os tipos de ponto de extremidade aninhada quando o perfil filho hello está no hello **parado** ou **desabilitado** estado.
- Se um ponto de extremidade exibe um **desabilitado** status, ele não será incluído na região Olá processo de correspondência. Esse comportamento também é aplicável para os tipos de ponto de extremidade aninhada ao ponto de extremidade de saudação é Olá **desabilitado** estado.
- Se uma consulta estiver vindo proveniente de uma região geográfica que não tenha mapeamento no perfil, o Gerenciador de Tráfego retornará uma resposta NODATA. Portanto, é altamente recomendável que os clientes usem o roteamento geográfico com um ponto de extremidade, o ideal é do tipo aninhado pelo menos dois pontos de extremidade no perfil de filho hello, com a região Olá **World** atribuído tooit. Isso também garante que os endereços IP que não mapeiam tooa região são manipulados.

Como explicamos em [Como funciona o Gerenciador de Tráfego](traffic-manager-how-traffic-manager-works.md), o Gerenciador de Tráfego não recebe consultas DNS diretamente de clientes. Em vez disso, as consultas DNS provenientes de serviço DNS recursivo Olá clientes Olá são toouse configurado. Portanto, Olá IP endereço usado toodetermine Olá região não é Olá o endereço IP do cliente, mas ele é o endereço IP de saudação do serviço DNS recursivo hello. Na prática, esse endereço IP é um proxy válido para cliente hello.


## <a name="next-steps"></a>Próximas etapas

Saiba como aplicativos de alta disponibilidade toodevelop usando [monitoramento de ponto de extremidade do Traffic Manager](traffic-manager-monitoring.md)

Saiba como muito[criar um perfil do Gerenciador de tráfego](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



