---
title: "aaaAuto dimensionar um serviço de nuvem no portal de saudação | Microsoft Docs"
description: "Saiba como toouse Olá tooconfigure portal regras de escala automática para uma função de web do serviço de nuvem ou uma função de trabalho no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Como tooconfigure automaticamente a escala para um serviço de nuvem no portal de saudação
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-scale-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-scale.md)

As condições podem ser definidas para uma função de trabalho de serviço de nuvem que dispara uma operação para reduzir ou escalar horizontalmente. condições de saudação para função hello podem se basear Olá CPU, disco ou da função de saudação de carga de rede. Você também pode definir uma condição com base na métrica de fila ou hello mensagem de alguns outros recursos do Azure associado à sua assinatura.

> [!NOTE]
> Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem. Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem. Você pode dimensionar uma máquina virtual padrão ao associá-la a um [conjunto de disponibilidade](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e ligá-los ou desligá-los manualmente.

## <a name="considerations"></a>Considerações
Você deve considerar Olá informações a seguir antes de configurar o dimensionamento para seu aplicativo:

* A colocação em escala é afetada pelo uso de núcleo.

    As instâncias de função maiores usam mais núcleos. Você pode dimensionar um aplicativo somente no limite de saudação de núcleos para sua assinatura. Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos. Se você executar um aplicativo com dois serviços de nuvem de médio porte (um total de 4 núcleos), você somente poderá expandir outras implantações de serviço de nuvem em sua assinatura por 16 núcleos de saudação restantes. Para saber mais sobre os tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).

* Você pode dimensionar com base em um limite de mensagens da fila. Para obter mais informações sobre como toouse filas, consulte [como toouse Olá serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Você também pode dimensionar outros recursos associados à sua assinatura.

* tooenable alta disponibilidade do seu aplicativo, você deve garantir que ele seja implantado com duas ou mais instâncias de função. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Onde a escala está localizada
Depois de selecionar o serviço de nuvem, você deve ter folha de serviço de nuvem de saudação visível.

1. Na folha de serviço de nuvem hello, em Olá **funções e instâncias** lado a lado, o nome de select Olá Olá do serviço de nuvem.   
   **IMPORTANTE**: tornar-se de que tooclick Olá função de serviço, não Olá instância de função que está abaixo da função hello.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Selecione Olá **escala** lado a lado.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Escala automática
Você pode definir as configurações de escala para uma função com o modo **manual** ou **automático**. Manual é conforme o esperado, você definir número absoluto de Olá de instâncias. Automático porém permite tooset regras que controlam como e por como muito você deverá fazer o dimensionamento.

Saudação de conjunto **o dimensionamento por** opção muito**regras de agendamento e desempenho**.

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Um perfil existente.
2. Adicione uma regra para o perfil do hello pai.
3. Adicione outro perfil.

Selecione **Adicionar Perfil**. perfil Hello determina qual modo você deseja toouse para escala Olá: **sempre**, **recorrência**, **data fixa**.

Depois que você configurou o perfil de saudação e regras, selecione Olá **salvar** no hello superior.

#### <a name="profile"></a>Perfil
mínimo de conjuntos de perfis de saudação e escala de instâncias máxima para hello e também quando esse intervalo de escala está ativo.

* **Sempre**

    Sempre mantenha esse intervalo de instâncias disponível.  

    ![Serviço de nuvem que sempre dimensiona](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Recorrência**

    Escolha um conjunto de dias de saudação semana tooscale.

    ![Escala de serviço de nuvem com um agendamento de recorrência](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Data Fixa**

    Uma função de saudação do data fixa intervalo tooscale.

    ![Escala de serviço de nuvem com uma data fixa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Depois de configurar o perfil de saudação, selecione Olá **Okey** botão na parte inferior da saudação da folha de perfil de saudação.

#### <a name="rule"></a>Regra
As regras são adicionadas tooa perfil e representam uma condição que dispara a escala de saudação.

gatilho de regra Olá baseia-se uma métrica de saudação do serviço de nuvem (utilização da CPU, atividade de disco ou atividade de rede) toowhich, você pode adicionar um valor condicional. Além disso, você pode ter gatilho Olá com base em uma métrica de saudação ou fila de mensagem de alguns outros recursos do Azure associado à sua assinatura.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Depois de configurar a regra de saudação, selecione Olá **Okey** botão na parte inferior da saudação da folha de regra de saudação.

## <a name="back-toomanual-scale"></a>Escala de toomanual back
Navegue toohello [as configurações de escala](#where-scale-is-located) e conjunto hello **o dimensionamento por** opção muito**uma contagem de instâncias que inseri manualmente**.

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Essa configuração remove o dimensionamento automatizadas de função hello e, em seguida, você pode definir a contagem de instâncias Olá diretamente.

1. opção de escala (manual ou automatizada) do Hello.
2. Uma saudação tooset de controle deslizante de instância de função tooscale para as instâncias.
3. Instâncias de saudação função tooscale para.

Depois de configurar as configurações de dimensionamento hello, selecione Olá **salvar** no hello superior.
