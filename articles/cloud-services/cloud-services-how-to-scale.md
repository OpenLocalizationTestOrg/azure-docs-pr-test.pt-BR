---
title: "aaaAuto dimensionar um serviço de nuvem no portal clássico Olá | Microsoft Docs"
description: "(clássico) Saiba como toouse Olá tooconfigure portal clássico regras de escala automática para uma função de web do serviço de nuvem ou uma função de trabalho no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Como tooconfigure automaticamente a escala para um serviço de nuvem no portal clássico Olá
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-scale-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-scale.md)

Na página de escala de saudação do hello portal clássico do Azure, você pode configurar as configurações de dimensionamento automático para sua função web ou função de trabalho. Como alternativa, você pode configurar a colocação em escala manual em vez da colocação em escala automática com base em regras.

> [!NOTE]
> Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem. Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem. Algumas dessas informações se aplica a tipos de toothese de máquinas virtuais. Dimensionamento de um conjunto de disponibilidade das máquinas virtuais é apenas sendo-los e desativar com base nas regras de escala Olá configurados. Para obter mais informações sobre máquinas virtuais e conjuntos de disponibilidade, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Você deve considerar Olá informações a seguir antes de configurar o dimensionamento para seu aplicativo:

* A colocação em escala é afetada pelo uso de núcleo.

    As instâncias de função maiores usam mais núcleos. Você pode dimensionar um aplicativo somente no limite de saudação de núcleos para sua assinatura. Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos. Se você executar um aplicativo com dois serviços de nuvem de médio porte (um total de 4 núcleos), você somente poderá expandir outras implantações de serviço de nuvem em sua assinatura por 16 núcleos de saudação restantes. Para saber mais sobre os tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).

* Você deve criar uma fila e associá-la a uma função antes de dimensionar um aplicativo com base em um limite de mensagens. Para obter mais informações, consulte [como toouse Olá serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Você pode dimensionar os recursos que estão vinculado tooyour serviço de nuvem. Para obter mais informações sobre a vinculação de recursos, consulte [como: vincular a um serviço de nuvem do recurso tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable alta disponibilidade do seu aplicativo, você deve garantir que ele seja implantado com duas ou mais instâncias de função. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Agendar o dimensionamento
Por padrão, nenhuma função segue um agendamento específico. Portanto, quaisquer configurações alteradas aplicam tooall vezes e todos os dias durante o ano de saudação. Se desejar, você pode configurar a expansão do manual ou automática para um dos modos a seguir de saudação:

* Dias da semana
* Finais de semana
* Noites da semana
* Manhãs da semana
* Datas específicas
* Intervalos de datas específicos

Olá agenda está definida no hello [portal clássico do Azure](https://manage.windowsazure.com/) em Olá  
**Serviços de Nuvem** > **\[Seu serviço de nuvem\]** > **Escala** > **\[Produção ou preparo\]**.

Clique em Olá **configurar horas agendadas** botão para cada função você deseja toochange.

![Dimensionamento automático do serviço de nuvem baseado em uma agenda][scale_schedules]

## <a name="manual-scale"></a>Dimensionamento manual
Em Olá **escala** página, você pode manualmente aumentar ou diminuir o número de saudação de instâncias em execução em um serviço de nuvem. Essa configuração é definida para cada agenda que você criou ou tooall tempo se você não tiver criado uma agenda.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
   
   > [!TIP]
   > Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.

2. Clique em **Escala**.
3. Selecione a agenda de saudação desejado toochange opções de dimensionamento para. *Não horários agendados* é o padrão de saudação se você não tiver nenhuma agenda foi definida.
4. Localize Olá **escala por métrica** seção e selecione **NONE**. Essa configuração é o padrão de saudação para todas as funções.
5. Cada função no serviço de nuvem Olá tem um controle deslizante para alterar o número de saudação do toouse de instâncias.
   
    ![Dimensionar manualmente uma função de serviço de nuvem][manual_scale]
   
    Se você precisar de mais instâncias, talvez seja necessário Olá toochange [tamanho da máquina virtual de serviço de nuvem](cloud-services-sizes-specs.md).
6. Clique em **Salvar**.  
   As instâncias de função são adicionadas ou removidas com base nas suas seleções.

> [!TIP]
> Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.

## <a name="automatic-scale---cpu"></a>Dimensionamento automático - CPU
Esse modo pode ser dimensionado se a porcentagem média de saudação do uso de CPU fica acima ou abaixo os limites especificados. As instâncias de função são criadas ou excluídas quando isso acontece.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
   
   > [!TIP]
   > Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.

2. Clique em **Escala**.
3. Selecione a agenda de saudação desejado toochange opções de dimensionamento para. *Não horários agendados* é o padrão de saudação se você não tiver nenhuma agenda foi definida.
4. Localize Olá **escala por métrica** seção e selecione **CPU**.
5. Agora você pode configurar um intervalo mínimo e máximo de instâncias de função, o uso de CPU de destino de hello (tootrigger a expansão vertical) e quantas instâncias tooscale ativo e inativo por.

![Dimensionar uma função de serviço de nuvem por carga de cpu][cpu_scale]

> [!TIP]
> Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.

## <a name="automatic-scale---queue"></a>Dimensionamento automático - fila
Esse modo dimensiona automaticamente se o número de saudação de mensagens em uma fila fica acima ou abaixo do limite especificado. As instâncias de função são criadas ou excluídas quando isso acontece.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
   
   > [!TIP]
   > Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.

2. Clique em **Escala**.
3. Localize Olá **escala por métrica** seção e selecione **fila**.
4. Agora você pode configurar um intervalo mínimo e máximo de instâncias de funções, fila hello e número de tooprocess de mensagens de fila para cada instância e quantos tooscale de instâncias para cima e para baixo por.

![Dimensionar uma função de serviço de nuvem por fila de mensagens][queue_scale]

> [!TIP]
> Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.

## <a name="scale-linked-resources"></a>Dimensionar recursos vinculados
Muitas vezes, quando você dimensionar uma função, é vantajoso tooscale Olá banco de dados usando o aplicativo hello é também. Se você vincular um serviço de nuvem em toohello Olá banco de dados, você pode acessar Olá escala configurações para esse recurso ao clicar no link apropriado hello.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
   
   > [!TIP]
   > Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.

2. Clique em **Escala**.
3. Localize Olá **recursos vinculados** seção e clique em **gerenciar escala para este banco de dados**.
   
   > [!NOTE]
   > Caso você não veja uma seção **recursos vinculados** , é provável que você não tenha recursos vinculados.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
