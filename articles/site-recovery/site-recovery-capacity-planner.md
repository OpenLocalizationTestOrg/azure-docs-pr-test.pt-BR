---
title: "capacidade de replicação aaaEstimate no Azure | Microsoft Docs"
description: Usar essa capacidade do artigo tooestimate ao replicar com o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Planejar a capacidade de proteger máquinas virtuais e o servidor físico no Azure Site Recovery

Olá Planejador de capacidade de recuperação de Site do Azure ferramenta ajuda a toofigure seus requisitos de capacidade ao replicar máquinas virtuais do Hyper-V, máquinas virtuais do VMware e servidores físicos do Windows/Linux, com o Azure Site Recovery.

Usar Olá Planejador de capacidade de recuperação de Site tooanalyze seu ambiente de origem e cargas de trabalho, estimar as necessidades de largura de banda e recursos de servidor, que será necessário para o local de origem hello e recursos de saudação (máquinas virtuais e armazenamento etc), que você precisa no destino Olá local.

Você pode executar a ferramenta de saudação em dois modos:

* **Planejando rápido**: executar ferramenta Olá nesse modo tooget projeções de rede e servidor com base em um número médio de VMs, discos, armazenamento e a taxa de alteração.
* **Planejamento detalhado**: execute a ferramenta de saudação nesse modo e fornecer detalhes de cada carga de trabalho no nível da VM. Analise a compatibilidade da VM e obtenha as projeções de rede e de servidor.

## <a name="before-you-start"></a>Antes de começar


1. Reúna informações sobre seu ambiente, inclusive VMs, discos por VM e armazenamento por disco.
2. Identifique sua taxa de alteração (variação) diária de dados replicados. toodo isso:

   * Se você estiver replicando máquinas virtuais do Hyper-V, faça o download Olá [ferramenta de planejamento de capacidade de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tooget taxa de alteração de saudação. [Saiba mais](site-recovery-capacity-planning-for-hyper-v-replication.md) sobre essa ferramenta. Recomendamos que você execute essa ferramenta em uma semana toocapture médias.
   * Se você estiver replicando máquinas virtuais VMware, use Olá [planejamento de implantação de recuperação de Site do Azure](./site-recovery-deployment-planner.md) toofigure out Olá taxa de variação.
   * Se você estiver replicando servidores físicos, você precisa tooestimate manualmente.

## <a name="run-hello-quick-planner"></a>Executar Olá Planejador rápida
1. Baixe e abra Olá [Planejador de capacidade de recuperação de Site do Azure](http://aka.ms/asr-capacity-planner-excel) ferramenta. Você precisa toorun macros, edição tooenable escolha e habilitar conteúdo quando solicitado.
2. Em **selecione um tipo de Planejador** selecione **Planejador rápido** Olá na caixa da lista.

   ![Introdução](./media/site-recovery-capacity-planner/getting-started.png)
3. Em Olá **Capacity Planner** planilha, insira informações Olá necessário. Preencha todos os campos de saudação dentro de um círculo em vermelho na captura de tela de saudação abaixo.

   * Em **selecionar seu cenário**, escolha **Hyper-V tooAzure** ou **tooAzure VMware/físicos**.
   * Em **(%) de taxa de alteração de dados diários médios**, coloque em informações de saudação reunidas usando Olá [ferramenta de planejamento de capacidade de Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) ou hello [planejamento da implantação de recuperação de Site do Azure](./site-recovery-deployment-planner.md).  
   * **Compactação** só se aplica toocompression oferecido ao replicar máquinas virtuais do VMware ou tooAzure de servidores físicos. Estimamos que 30% ou mais, mas você pode modificar a configuração de saudação conforme necessário. Para replicar máquinas virtuais do Hyper-V tooAzure compactação, você pode usar um utilitário de terceiros, como Riverbed.
   * Em **Entradas de Retenção**, especifique por quanto tempo as réplicas devem ser retidas. Olá valor de entrada se você estiver replicando VMware ou servidores físicos, em dias. Se você estiver replicando Hyper-V, especifique o tempo de saudação em horas.
   * No **número de horas em que a replicação inicial para o lote de saudação de máquinas virtuais deve ser concluídas** e **número de máquinas virtuais por lote de replicação inicial**, insira as configurações que são usadas requisitos de replicação inicial de toocompute.  Quando a recuperação de Site é implantada, Olá conjunto inicial de dados deve ser carregado.

   ![Entradas](./media/site-recovery-capacity-planner/inputs.png)
4. Depois de você colocar valores Olá para o ambiente de origem hello, a saída exibida inclui:

   * **Largura de banda necessária para a replicação delta** (MB/s). Largura de banda de rede para replicação delta é calculada em média taxa diário de alteração de dados hello.
   * **Largura de banda necessária para a replicação inicial** (MB/s). Largura de banda de rede para a replicação inicial será calculada em valores de replicação inicial de saudação em que colocar.
   * **Armazenamento necessário (em GBs)** é o armazenamento do Azure total Olá necessário.
   * **Total de IOPS em contas de armazenamento padrão** é calculado com base no tamanho da unidade de 8K IOPS em contas de armazenamento padrão total hello.  Para Olá Planejador rápida, número de saudação é calculado com base em todos os discos de máquinas virtuais de origem hello e diariamente taxa de alteração de dados. Para Olá Planejador detalhadas, número de saudação é calculado com base no número total de máquinas virtuais que são mapeada toostandard VMs do Azure e taxa nessas VMs de alteração de dados.
   * **Número de contas de armazenamento padrão** fornece o número total de saudação de armazenamento padrão contas necessárias tooprotect Olá VMs. Uma conta de armazenamento padrão pode conter o IOPS too20000 em todas as VMs de saudação em um armazenamento padrão e um máximo de 500 IOPS com suporte por disco.
   * **Número de discos de blob necessário** fornece Olá número de discos que será criado no armazenamento do Azure.
   * **Número de contas de armazenamento premium necessário** fornece o número total de saudação do tooprotect de contas necessárias de armazenamento premium Olá VMs. Uma VM de origem com IOPS alto (acima de 20 mil) precisa de uma conta de armazenamento premium. Uma conta de armazenamento premium pode conter backup too80000 IOPS.
   * **Total de IOPS em armazenamento premium** é calculado com base no tamanho da unidade de 256 K IOPS em contas de armazenamento total premium Olá.  Para Olá Planejador rápida, número de saudação é calculado com base em todos os discos de máquinas virtuais de origem hello e diariamente taxa de alteração de dados. Para Olá Planejador detalhadas, Olá é calculada Olá com base no número total de máquinas virtuais que são mapeada toopremium VM do Azure (série GS e DS) e dados de saudação alterar taxa nessas VMs.
   * **Número de servidores de configuração necessários** mostra quantos servidores de configuração são necessários para a implantação de saudação.
   * **Número de servidores de processo adicional necessário** mostra se os servidores de processo adicional são necessários, no servidor de processo do toohello adição é executado no servidor de configuração de saudação por padrão.
   * **armazenamento adicional de 100% em fonte Olá** mostra se o armazenamento adicional é necessária no local de origem hello.

   ![Saída](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Executar Olá detalhadas Planejador

1. Baixe e abra Olá [Planejador de capacidade de recuperação de Site do Azure](http://aka.ms/asr-capacity-planner-excel) ferramenta. Você precisa toorun macros, edição tooenable escolha e habilitar conteúdo quando solicitado.
2. Em **selecione um tipo de Planejador**, selecione **Planejador detalhadas** Olá na caixa da lista.

   ![Introdução](./media/site-recovery-capacity-planner/getting-started-2.png)
3. Em Olá **qualificação de carga de trabalho** planilha, insira informações Olá necessário. Você deve preencher todas as Olá marcado como campos.

   * Em **núcleos de processador**, especifique o número total de saudação de núcleos em um servidor de origem.
   * Em **alocação de memória em MB**, especifique o tamanho Olá RAM de um servidor de origem.
   * Olá **número de NICs**, especifique o número de saudação de adaptadores de rede em um servidor de origem.
   * Em **Total de armazenamento (em GB)**, especifique o tamanho total de saudação do armazenamento de máquina virtual de saudação. Por exemplo, se o servidor de origem Olá tem 3 discos com 500 GB, o tamanho de armazenamento total é 1.500 GB.
   * Em **número de discos anexados**, especifique o número total de saudação de discos de um servidor de origem.
   * Em **a utilização da capacidade do disco**, especifique a média de utilização de saudação.
   * Em **diariamente alterar taxa (%)**, especificar dados diários Olá alterar a taxa de um servidor de origem.
   * Em **tamanho mapeamento Azure**, insira o tamanho da VM Azure Olá que você deseja toomap. Se você não quiser toodo nesse manualmente, clique em **de computação VMs de IaaS**. Se uma configuração manual de entrada e, em seguida, clique em computação de VMs de IaaS, a configuração manual de saudação pode ser substituída porque o processo de computação Olá identifica automaticamente o melhor correspondência Olá no tamanho da VM do Azure.

   ![Qualificação de Carga de Trabalho](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Se você clicar em **VMs IaaS de Computação** , isso é o que essa opção faz:

   * Valida entradas obrigatórias hello.
   * Calcula o IOPS e sugere Olá aize de VM do Azure melhor correspondência para cada VMs que está qualificada para a replicação tooAzure. Se não for possível detectar um tamanho adequado de VM do Azure, um erro será emitido. Por exemplo, se o número de saudação de discos anexados 65, é emitido um erro porque o tamanho do maior Olá VM do Azure é 64.
   * Sugere uma conta de armazenamento que pode ser usada para uma VM do Azure.
   * Calcula o número total de saudação de contas de armazenamento padrão e contas de armazenamento premium necessárias para carga de trabalho de saudação. Role para baixo Olá tooview tipo de armazenamento do Azure e a conta de armazenamento de saudação que pode ser usada para um servidor de origem.
   * Conclusão e classifica restante Olá Olá tabela com base no tipo de armazenamento necessária (standard ou premium) atribuído para uma VM e o número de saudação de discos anexados. Para todas as VMs que atendem aos requisitos de saudação do Azure, Olá coluna **VM é qualificado?** mostra **Sim**. Se uma máquina virtual não pode ser feita tooAzure, um erro será exibido.

Colunas AA tooAE são produzidas e fornecem informações para cada VM.

![Qualificação de Carga de Trabalho](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Exemplo
Por exemplo, para seis VMs com valores hello mostrados na tabela Olá, ferramenta de Olá calcula e atribui a melhor correspondência de VM do Azure hello e requisitos de armazenamento do Azure hello.

![Qualificação de Carga de Trabalho](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Na saída do exemplo hello, observe o seguinte hello:

  * Olá primeira coluna é uma coluna de validação para VMs hello, discos e variação.
  * São necessárias duas contas de armazenamento padrão e uma conta de armazenamento premium para cinco VMs.
  * A VM3 não se qualifica para proteção, pois um ou mais discos tem mais de 1 TB.
  * VM1 e VM2 podem usar a primeira conta de armazenamento padrão Olá
  * VM4 pode usar a segunda conta de armazenamento padrão hello.
  * A VM5 e a VM6 precisam de uma conta de armazenamento premium e podem usar a mesma conta.

    > [!NOTE]
    > IOPS no armazenamento standard e premium são calculados em Olá nível da VM e não no nível de disco. Uma máquina virtual padrão pode manipular o too500 IOPS por disco. Se o IOPS de um disco for maior que 500, você precisará do armazenamento premium. No entanto, se o IOPS de um disco de mais de 500, mas IOPS para discos de VM total Olá estão dentro de saudação suporte limites padrão de VM do Azure (tamanho da VM, número de discos, número de memória de adaptadores, CPU,), planejador Olá escolhe uma VM e não hello DS ou GS série padrão. Você precisa de célula de tamanho do Azure de mapeamento de saudação atualização toomanually com série DS ou GS apropriado VM.


Depois que todos os detalhes de saudação entram em vigor, clique em **ferramenta Planejador a enviar dados toohello** tooopen Olá **Capacity Planner** cargas de trabalho realçado, tooshow se eles são qualificados para proteção ou não.

### <a name="submit-data-in-hello-capacity-planner"></a>Enviar dados em Olá Planejador de capacidade
1. Quando você abre Olá **Capacity Planner** planilha é populada com base nas configurações de saudação que você especificou. Olá palavra 'Carga de trabalho' aparece em Olá **origem de entradas de infra-estrutura** célula, tooshow que Olá entrada é hello **qualificação de carga de trabalho** planilha.
2. Se você quiser toomake alterações, você precisa toomodify Olá **qualificação de carga de trabalho** planilha e clique em **ferramenta Planejador a enviar dados toohello** novamente.  

   ![Planejador de Capacidade](./media/site-recovery-capacity-planner/capacity-planner.png)
