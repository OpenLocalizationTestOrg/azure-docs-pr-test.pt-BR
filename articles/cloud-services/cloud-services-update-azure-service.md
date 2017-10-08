---
title: "aaaHow tooupdate um serviço de nuvem | Microsoft Docs"
description: "Saiba como os serviços de nuvem tooupdate no Azure. Saiba como uma atualização em um serviço de nuvem continuará tooensure disponibilidade."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Como tooupdate um serviço de nuvem

A atualização de um serviço de nuvem, incluindo suas funções e o SO convidado, é um processo que envolve três etapas. Primeiro, os binários de saudação e arquivos de configuração para Olá novo serviço de nuvem ou versão do sistema operacional deve ser carregado. Em seguida, o Azure reservará recursos de computação e rede para o serviço de nuvem Olá com base nos requisitos de saudação da nova versão de serviço de nuvem hello. Por fim, o Azure executa um sem interrupção tooincrementally atualização Olá locatário toohello nova versão de atualização ou o SO, enquanto preserva sua disponibilidade. Este artigo aborda os detalhes de saudação nesta última etapa – Olá atualização sem interrupção.

## <a name="update-an-azure-service"></a>Atualizar um serviço do Azure
O Azure organiza suas instâncias de função em agrupamentos lógicos chamados de domínios de atualização (UD). Os domínios de atualização (UD) são conjuntos lógicos de instâncias de função que são atualizados como um grupo.  Atualizações do Azure, uma nuvem de serviço um UD por vez, que permite que as instâncias em outros toocontinue UDs que serve o tráfego.

saudação padrão número de domínios de atualização é 5. Você pode especificar um número diferente de domínios de atualização, incluindo o atributo de upgradeDomainCount Olá no arquivo de definição do serviço da saudação (. csdef). Para obter mais informações sobre o atributo de upgradeDomainCount hello, consulte [esquema WebRole](https://msdn.microsoft.com/library/azure/gg557553.aspx) ou [esquema WorkerRole](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Quando você executa uma atualização in-loco de uma ou mais funções em seu serviço, o Azure atualiza conjuntos de instâncias de função de acordo com o toowhich de domínio de atualização toohello pertencem. Atualizações do Azure, todas as instâncias de saudação em um determinado domínio de atualização, interrompendo-as, atualizando-os, colocando-os online novamente, em seguida, move para o próximo domínio de saudação. Parando somente instâncias de saudação em execução em Olá atual domínio de atualização, o Azure garante que uma atualização ocorra com hello mínimo possível impacto toohello executando o serviço. Para obter mais informações, consulte [como atualização Olá continua](#howanupgradeproceeds) posteriormente neste artigo.

> [!NOTE]
> Embora os termos de saudação **atualizar** e **atualizar** tenham significados levemente diferentes no contexto de saudação do Azure, eles podem ser usados alternadamente para processos de saudação e descrições dos recursos de saudação neste documento.
>
>

O serviço deve definir pelo menos duas instâncias de uma função para essa função toobe atualizada in-loco sem tempo de inatividade. Se o serviço Olá consiste em apenas uma instância de uma função, seu serviço estará disponível até que hello atualização in-loco seja concluída.

Este tópico aborda Olá informações sobre atualizações do Azure a seguir:

* [Alterações permitidas no serviço durante uma atualização](#AllowedChanges)
* [Como uma atualização é realizada](#howanupgradeproceeds)
* [Reversão de uma atualização](#RollbackofanUpdate)
* [Inicialização de várias operações de mutação em uma implantação em andamento](#multiplemutatingoperations)
* [Distribuição de funções em domínios de atualização](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Alterações permitidas no serviço durante uma atualização
Olá tabela a seguir mostra Olá permitidas alterações tooa serviço durante uma atualização:

| Alterações permitidas toohosting, serviços e funções | Atualização in-loco | Em estágios (permuta de VIP) | Excluir e reimplantar |
| --- | --- | --- | --- |
| Versão do sistema operacional |Sim |Sim |Sim |
| Nível de confiança do .NET |Sim |Sim |Sim |
| Tamanho da máquina virtual<sup>1</sup> |Sim<sup>2</sup> |Sim |Sim |
| Configurações de armazenamento local |Apenas aumento<sup>2</sup> |Sim |Sim |
| Adicionar ou remover funções em um serviço |Sim |Sim |Sim |
| Número de instâncias de uma função específica |Sim |Sim |Sim |
| Número ou tipo de pontos de extremidade de um serviço |Sim<sup>2</sup> |Não |Sim |
| Nomes e valores dos parâmetros de configuração |Sim |Sim |Sim |
| Valores (mas não nomes) dos parâmetros de configuração |Sim |Sim |Sim |
| Adicionar novos certificados |Sim |Sim |Sim |
| Alterar certificados existentes |Sim |Sim |Sim |
| Implantar novo código |Sim |Sim |Sim |

<sup>1</sup> alterações de tamanho limitado toohello subconjunto de tamanhos disponíveis para o serviço de nuvem hello.

<sup>2</sup> Exige o Azure SDK 1.5 ou versões posteriores.

> [!WARNING]
> Alterar o tamanho da máquina virtual Olá destruirá os dados locais.
>
>

Olá itens a seguir não têm suporte durante uma atualização:

* Alterando o nome de saudação de uma função. Remova e adicione a função hello com novo nome de saudação.
* Alteração da saudação contagem de atualização do domínio.
* Diminuindo o tamanho de saudação dos recursos locais hello.

Se você estiver fazendo outras atualizações de definição do serviço tooyour, como a redução do tamanho de saudação do recurso local, você deve executar uma atualização de permuta de VIP em vez disso. Para saber mais, consulte, consulte [Implantação de permuta](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Como uma atualização é realizada
Você pode decidir se deseja tooupdate todas as funções hello em seu serviço ou uma única função no serviço de saudação. Em ambos os casos, todas as instâncias de cada função que está sendo atualizado e pertencem toohello primeiro domínio de atualização são interrompidas, atualizadas e volte a ficar online. Quando eles estiverem online novamente, hello instâncias no segundo domínio de atualização de saudação são interrompidas, atualizadas e volte a ficar online. Um serviço de nuvem pode ter no máximo uma atualização ativa por vez. atualização de saudação sempre é executada em relação à versão mais recente do Olá Olá do serviço de nuvem.

Olá diagrama a seguir ilustra como atualização Olá ocorre se você estiver atualizando todas as funções hello no serviço de saudação de:

![Atualizar serviço](media/cloud-services-update-azure-service/IC345879.png "Atualizar serviço")

Este próximo diagrama ilustra como atualização Olá continua se você estiver atualizando somente uma única função:

![Atualizar função](media/cloud-services-update-azure-service/IC345880.png "Atualizar função")  

Durante uma atualização automática, o Olá controlador de malha do Azure avalia periodicamente a integridade Olá de toodetermine de serviço de nuvem hello quando sua segurança toowalk Olá UD Avançar. A avaliação de integridade é executada em uma base por função e considera apenas as instâncias na versão mais recente da saudação (ou seja, instâncias de UDs já tem sido movimentadas). Ela verifica se um número mínimo de instâncias de função, para cada função, atingiu um estado de terminal satisfatório.

### <a name="role-instance-start-timeout"></a>Tempo limite de inicialização de instância de função
Olá controlador de malha aguardará 30 minutos para cada instância de função tooreach um estado iniciado. Se a duração do tempo limite de saudação expira, Olá controlador de malha continuará percorrer toohello próxima instância de função.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Dados de toodrive impacto durante as atualizações de serviço de nuvem

Ao atualizar um serviço de instâncias de toomultiple uma única instância seu serviço será interrompido enquanto Olá atualização é executada devido a maneira toohello Azure atualiza os serviços. Olá serviço contrato de nível garante disponibilidade do serviço se aplica somente a tooservices que são implantados com mais de uma instância. Olá lista a seguir descreve como os dados de saudação em cada unidade são afetados por cada cenário de atualização de serviço do Azure:

|Cenário|Unidade C|Unidade D|Unidade E|
|--------|-------|-------|-------|
|Reinicialização da VM|Preservado|Preservado|Preservado|
|Reinicialização do portal|Preservado|Preservado|Destruído|
|Nova imagem do Portal|Preservado|Destruído|Destruído|
|Atualização in-loco|Preservado|Preservado|Destruído|
|Migração de nó|Destruído|Destruído|Destruído|

Observe que, em Olá acima da lista, Olá unidade e: representa a unidade raiz da função hello e não deve ser inserido no código. Em vez disso, use Olá **% RoleRoot %** unidade de saudação do toorepresent variável de ambiente.

toominimize Olá tempo de inatividade ao atualizar um serviço de instância única, implantar um nova multi-instância serviço toohello servidor de preparo e executar uma permuta de VIP.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Reversão de uma atualização
O Azure fornece flexibilidade no gerenciamento de serviços durante uma atualização, permitindo que você inicie operações adicionais em um serviço, após a saudação inicial atualizar a solicitação é aceita pelo Olá controlador de malha do Azure. Uma reversão só pode ser executada quando uma atualização (alteração de configuração) ou atualização está em Olá **em andamento** estado na implantação de saudação. Uma atualização ou upgrade é considerada toobe em andamento, desde que exista pelo menos uma instância do serviço de saudação que ainda não foram atualizados toohello nova versão. tootest se uma reversão é permitida, verifique o valor de saudação do sinalizador de RollbackAllowed hello, retornado por [obter a implantação](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [obter propriedades do serviço de nuvem](https://msdn.microsoft.com/library/azure/ee460806.aspx) operações, é definir tootrue.

> [!NOTE]
> Só faz sentido toocall Rollback em uma **in-loco** atualização ou upgrade pois as atualizações de permuta de VIP envolvem a substituição de uma instância em execução inteira de seu serviço com outra.
>
>

Reversão de uma atualização em andamento tem Olá efeitos na implantação Olá a seguir:

* Quaisquer instâncias de função que ainda não tiveram sido atualizada ou atualizados toohello nova versão não são atualizadas ou atualizadas, porque essas instâncias já estiver executando a versão de destino de saudação do serviço de saudação.
* Instâncias de qualquer função que já tinha sido atualizado ou atualizado toohello nova versão do pacote de serviço hello (\*. cspkg) hello ou arquivo de configuração de serviço (\*. cscfg) arquivo (ou ambos) estão na versão de pré-atualização toohello revertido de Esses arquivos.

Essa funcionalidade é fornecida pelo Olá recursos a seguir:

* Olá [reversão de atualização ou atualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operação, que pode ser chamada em uma atualização de configuração (disparada pela chamada [alterar configuração de implantação](https://msdn.microsoft.com/library/azure/ee460809.aspx)) ou uma atualização (disparado pela chamada [ Implantação de atualização](https://msdn.microsoft.com/library/azure/ee460793.aspx)) como há pelo menos uma instância no serviço de saudação que ainda não foi atualizado toohello nova versão.
* Olá elemento bloqueado e elemento de RollbackAllowed hello, que são retornados como parte do corpo de resposta de saudação do hello [obter a implantação](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [obter propriedades do serviço de nuvem](https://msdn.microsoft.com/library/azure/ee460806.aspx) operações:

  1. Olá bloqueado elemento permite que você toodetect quando uma operação de mutação pode ser chamada em uma determinada implantação.
  2. Olá RollbackAllowed elemento permite que você toodetect quando hello [reversão atualização ou atualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operação pode ser chamada em uma determinada implantação.

  Em ordem tooperform uma reversão, você não tem toocheck Olá bloqueado tanto Olá elementos RollbackAllowed. Basta tooconfirm que RollbackAllowed está definida tootrue. Esses elementos são retornados apenas se esses métodos são chamados usando o cabeçalho da solicitação Olá definido muito "x-ms-version: 2011-10-01" ou uma versão posterior. Para saber mais sobre os cabeçalhos de controle de versão, consulte [Controle de versão do serviço de gerenciamento](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Há algumas situações nas quais não há suporte para uma reversão de uma atualização ou upgrade, entre elas:

* Redução em recursos locais - se Olá atualização aumenta Olá recursos locais para uma função hello plataforma Windows Azure não permitirá a reversão.
* Limitações de cota - se a atualização da saudação foi uma escala para baixo de operação, você pode não ter operação de reversão do suficientes computação cota toocomplete hello. Cada assinatura do Azure tem uma cota associada que especifica o número máximo de saudação de núcleos que podem ser consumidos por todos os serviços hospedados que pertencem a assinatura de toothat. Se a execução de uma reversão de uma determinada atualização colocar sua assinatura acima da cota, a reversão não será habilitada.
* Condição de corrida - se a atualização de saudação inicial foi concluída, uma reversão não é possível.

Um exemplo de quando a reversão de saudação de uma atualização pode ser útil é se você estiver usando Olá [implantação de atualização](https://msdn.microsoft.com/library/azure/ee460793.aspx) operação na taxa de saudação toocontrol de modo manual no qual o serviço hospedado um principal tooyour de atualização in-loco do Azure é distribuída.

Durante a distribuição de saudação da atualização Olá chamar [implantação de atualização](https://msdn.microsoft.com/library/azure/ee460793.aspx) no modo manual e começar toowalk domínios de atualização. Se em algum momento, como monitorar atualização hello, você observar algumas instâncias de função em Olá primeiro domínios de atualização que examina se tornaram sem resposta, você pode chamar hello [reversão atualização ou atualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operação na implantação de saudação que deixará instâncias Olá inalterados que ainda não foram atualizadas e reverterá as instâncias que foram atualizados toohello pacote de serviço anterior e a configuração.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Inicialização de várias operações de mutação em uma implantação em andamento
Em alguns casos pode ser tooinitiate várias operações de mutação simultâneas em uma implantação em andamento. Por exemplo, você pode executar uma atualização de serviço e, enquanto que a atualização está sendo revertida no seu serviço, você deseja toomake alguma alteração, por exemplo, tooroll Olá atualização, aplicar outra atualização ou até mesmo excluir a implantação de saudação. Um caso em que isso pode ser necessário é se uma atualização de serviço contém um código com bug que faz com que uma falha de toorepeatedly de instância de função atualizada. Nesse caso, a saudação controlador de malha do Azure não será toomake capaz de progresso na aplicação dessa atualização porque um número insuficiente de instâncias no domínio atualizado Olá está íntegro. Esse estado é chamado tooas um *implantação paralisada*. Você pode resolver implantação Olá reversão Olá atualização ou aplicando uma atualização recente pela parte superior da saudação falhando um.

Depois que o serviço de Olá Olá solicitação inicial tooupdate ou atualização foi recebido pelo Olá controlador de malha do Azure, você pode iniciar operações de mutação subsequentes. Ou seja, você não tem toowait para saudação inicial operação toocomplete antes de iniciar outra operação de mutação.

Iniciar uma segunda operação de atualização enquanto Olá primeira atualização está em andamento, você executará a operação de reversão toohello semelhante. Se Olá segunda atualização estiver em modo automático, Olá primeiro domínio de atualização serão atualizado imediatamente, possivelmente fazendo tooinstances de vários domínios de atualização fiquem offline no hello mesmo ponto no tempo.

Olá operações de mutação são as seguintes: [alterar configuração de implantação](https://msdn.microsoft.com/library/azure/ee460809.aspx), [implantação de atualização](https://msdn.microsoft.com/library/azure/ee460793.aspx), [Status de implantação de atualização](https://msdn.microsoft.com/library/azure/ee460808.aspx), [excluir Implantação](https://msdn.microsoft.com/library/azure/ee460815.aspx), e [atualização de reversão](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Duas operações, [obter a implantação](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [obter propriedades do serviço de nuvem](https://msdn.microsoft.com/library/azure/ee460806.aspx), retornam o sinalizador de bloqueado Olá que pode ser examinada toodetermine se uma operação de mutação pode ser chamada em uma determinada implantação.

Ordem toocall Olá versão desses métodos que retorna o sinalizador de bloqueado hello, você deve definir o cabeçalho de solicitação muito "x-ms-version: 2011-10-01" ou posterior. Para saber mais sobre os cabeçalhos de controle de versão, consulte [Controle de versão do serviço de gerenciamento](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Distribuição de funções em domínios de atualização
O Azure distribui instâncias de uma função uniformemente em um número definido de domínios de atualização, que pode ser configurado como parte do arquivo de definição (. csdef) do serviço de saudação. Olá o número máximo de domínios de atualização é 20 e saudação padrão é 5. Para obter mais informações sobre como toomodify Olá arquivo de definição de serviço, consulte [esquema de definição de serviço do Azure (arquivo. csdef)](cloud-services-model-and-package.md#csdef).

Por exemplo, se a sua função tiver dez instâncias, por padrão cada domínio de atualização conterá duas instâncias. Se sua função tiver 14 instâncias, quatro dos domínios de atualização Olá contêm três instâncias, e um quinto domínio conterá duas.

Domínios de atualização são identificados com um índice de base zero: Olá primeiro domínio de atualização tem uma ID de 0 e o segundo domínio de atualização Olá tem uma ID de 1 e assim por diante.

Olá diagrama a seguir ilustra como um serviço que contém duas funções são distribuídas ao serviço Olá define dois domínios de atualização. serviço de saudação está executando oito instâncias de função da web de saudação e nove instâncias da função de trabalho hello.

![Distribuição de domínios de atualização](media/cloud-services-update-azure-service/IC345533.png "Distribuição de domínios de atualização")

> [!NOTE]
> Observe que o Azure controla como as instâncias são alocadas nos domínios de atualização. Não é possível toospecify quais instâncias são alocadas toowhich domínio.
>
>

## <a name="next-steps"></a>Próximas etapas
[Como os serviços de nuvem tooManage](cloud-services-how-to-manage.md)  
[Como os serviços de nuvem tooMonitor](cloud-services-how-to-monitor.md)  
[Como os serviços de nuvem tooConfigure](cloud-services-how-to-configure.md)  
