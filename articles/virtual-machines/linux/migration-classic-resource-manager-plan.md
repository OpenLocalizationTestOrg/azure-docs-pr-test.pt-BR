---
title: "aaaPlanning para migração de recursos de IaaS de tooAzure clássico Resource Manager | Microsoft Docs"
description: "Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos
Enquanto o Gerenciador de recursos do Azure oferece muitos recursos incríveis, é crítico tooplan out seu toomake jornada de migração se as coisas suaves. Gastar tempo no planejamento garantirá que não ocorram problemas durante a execução das atividades de migração. 

> [!NOTE] 
> Olá diretrizes a seguir foi muito contribuído tooby hello Azure Customer Advisory team nuvem arquitetos de soluções e trabalhar com os clientes em migração enviornments grandes. Como tal, este documento continuará tooget atualizada à medida que novos padrões de sucesso surgir, por isso, verifique novamente pelo tempo tootime toosee se houver quaisquer recomendações novo.

Há quatro fases gerais de jornada de migração de saudação:

![Fases da migração](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Plano

### <a name="technical-considerations-and-tradeoffs"></a>Considerações técnicas e compensações

Dependendo do tamanho de requisitos técnicos, regiões geográficas e práticas operacionais, você pode desejar tooconsider:

1. Por que sua organização deseja usar o Azure Resource Manager?  Quais são os motivos dos negócios Olá para uma migração?
2. Quais são os motivos técnicos de saudação do Azure Resource Manager?  Quais (se houver) serviços adicionais do Azure você gostaria que tooleverage?
3. Aplicativo (ou conjuntos de máquinas virtuais) estão incluídos na migração Olá?
4. Quais cenários são suportados com a API de migração de Olá?  Saudação de revisão [sem suporte a recursos e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations).
5. As equipes operacionais agora darão suporte a aplicativos/VMs no Clássico e no Azure Resource Manager?
6. Como o Azure Resource Manager altera seus processos de implantação, gerenciamento, monitoramento e relatório da VM (se houver)?  Os scripts de implantação são necessário toobe atualizado?
7. O que é comunicações Olá planeja tooalert participantes (os usuários finais, os proprietários de aplicativos e proprietários de infraestrutura)?
8. Dependendo da complexidade de saudação do ambiente hello, deve haver um período de manutenção em que o aplicativo hello é tooend indisponível usuários e proprietários de tooapplication?  Em caso afirmativo, por quanto tempo?
9. Os participantes de tooensure de plano de treinamento Olá são proficientes no Gerenciador de recursos do Azure e experientes?
10. O que é o gerenciamento de programa hello ou plano de gerenciamento de projeto para a migração de Olá?
11. Quais são os cronogramas de saudação para migração do Azure Resource Manager hello e outros relacionados mapas de trânsito de tecnologia?  Eles estão alinhados corretamente?

### <a name="patterns-of-success"></a>Padrões de sucesso

Clientes bem-sucedidos têm planos onde hello acima perguntas são discutidas, documentado e controlado detalhados.  Certifique-se de planos de migração de saudação são amplamente comunicados toosponsors e participantes.  Esteja munido com o conhecimento sobre as opções de migração; é altamente recomendável ler todo este conjunto de documentos sobre migração abaixo.

* [Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS toomigrate CLI do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Armadilhas tooavoid

- Tooplan de falha.  etapas de tecnologia Olá dessa migração comprovadamente e resultado Olá é previsível.
- Supondo que Olá plataforma suportada migração API será conta para todos os cenários. Saudação de leitura [sem suporte a recursos e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand quais cenários são suportados.
- Não planejar a possível interrupção do aplicativo para os usuários finais.  Planejar o buffer suficiente tooadequately avisar os usuários finais do tempo de aplicativos potencialmente não está disponível.


## <a name="lab-test"></a>Teste de laboratório 

**Replicar o ambiente e fazer uma migração de teste**
  > [!NOTE]
  > A replicação exata do ambiente existente é executada com uma ferramenta que é uma contribuição da comunidade, sem suporte oficial do Suporte da Microsoft. Portanto, é um **opcional** etapa mas é melhor toofind de maneira Olá problema sem tocar em seus ambientes de produção. Se não for uma opção de usar uma ferramenta contribuído pela comunidade, em seguida, leia sobre Olá recomendação de simulação de preparação/validar/Abort abaixo.
  >
  
  Realizar um laboratório de teste do seu cenário exato (computação, rede e armazenamento) é tooensure de maneira melhor de saudação uma migração tranquila. Isso ajuda a garantir que:

  - Um laboratório totalmente separado ou um tootest do ambiente de produção não existente. Recomendamos ter um laboratório totalmente separado que pode ser migrado repetidamente e modificado de forma destrutiva.  Metadados de toocollect/hydrate scripts de assinaturas real Olá estão listadas abaixo.
  - É um laboratório de saudação boa ideia toocreate em uma assinatura separada. Olá razão é que laboratório Olá será interrompido repetidamente, e ter um separado, assinatura isolada reduzirá chance de saudação que algo real obterá acidentalmente excluídos.

  Isso pode ser feito usando a ferramenta de AsmMetadataParser hello. [Leia mais sobre essa ferramenta aqui](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Padrões de sucesso

a seguir Olá foram problemas descobertos em muitas das migrações maior hello. Isso não é uma lista completa, e você deverá consultar toohello [sem suporte a recursos e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) para obter mais detalhes. Você poderá ou não ter estes problemas técnicos, mas se tiver, resolvê-los antes de tentar realizar a migração garantirá uma experiência mais tranquila.

- **Faça uma execução de teste de preparação/validar/Abort** -essa é talvez hello mais importante etapa tooensure clássico tooAzure Gerenciador de recursos sucesso da migração. migração de saudação API tem três etapas principais: validar, preparar e confirmar. Validar será leitura do estado de saudação do seu ambiente clássico e retornar um resultado de todos os problemas. No entanto, porque talvez haja alguns problemas na pilha do Gerenciador de recursos do Azure hello, validar não pode capturar tudo. a próxima etapa no processo de migração Hello, preparação ajudará a expor esses problemas. Preparar irá mover Olá metadados do clássico tooAzure Gerenciador de recursos, mas será confirmação não Olá movimento e será não remover ou alterar qualquer coisa no hello lado clássico. Olá simulação envolve a preparação de migração hello, em seguida, anulando (**sem confirmação**) preparar migração hello. Olá objetivo validar/preparar/abort simulação é toosee todos os metadados de saudação na pilha do Gerenciador de recursos do Azure hello, examiná-lo (*programaticamente ou no Portal*), verifique se tudo migra corretamente e trabalhar com problemas técnicos.  Ela também lhe dará uma ideia da duração da migração, de forma que você possa planejar o tempo de inatividade de acordo.  Um validar/preparar/abort não causa nenhum tempo de inatividade do usuário; Portanto, é o uso de tooapplication sem interrupções.
  - itens de saudação abaixo precisará toobe resolvido antes de simulação hello, mas um teste de simulação com segurança liberará essas etapas de preparação, se eles estão ausentes. Durante a migração da empresa, que encontramos Olá simulação toobe uma preparação de migração do modo seguro e inestimável tooensure.
  - Preparar quando estiver em execução, o controle de saudação plano (operações de gerenciamento do Azure) será bloqueado para Olá toda rede virtual, e portanto não pode fazer alterações tooVM metadados durante a validar/preparar/abort.  Mas, de outro modo, a função de qualquer aplicativo (RD, uso da VM, etc.) não será afetada.  Os usuários de VMs Olá não saberá que simulação hello está sendo executada.

- **Circuitos do ExpressRoute e VPN**. Atualmente, os Gateways do ExpressRoute com links de autorização não podem ser migrados sem tempo de inatividade. Para solucionar esse problema hello, consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Extensões de VM** -extensões de máquina Virtual são potencialmente uma saudação maiores obstáculos toomigrating VMs em execução. A correção das Extensões de VM pode levar mais de 1 a 2 dias; portanto, planeje de forma adequada.  Um trabalho do agente do Azure é necessário tooreport back status de extensão de VM de VMs em execução. Se o status de saudação voltar como inválido para uma VM em execução, isso interromperá a migração. próprio agente de saudação não precisa toobe em funcionamento tooenable migração, mas se houver extensões no hello VM, e ambos um agente de trabalho e saída conectividade com a internet (com DNS) serão necessárias para encaminhar toomove de migração.
  - Se o servidor DNS tooa conectividade for perdida durante a migração, todas as extensões de VM exceto BGInfo v1. \* necessário toofirst ser removido de cada VM antes de preparação da migração e subsequentemente adicionado novamente toohello back VM após a migração do Gerenciador de recursos do Azure.  **Isso se refere apenas às VMs em execução.**  Se Olá VMs forem interrompido desalocada, extensões de VM não é necessário toobe removido. **Observação:** várias extensões como o diagnóstico do Azure e o monitoramento da central de segurança serão reinstalados automaticamente após a migração e, portanto, removê-las não será um problema.
  - Além disso, verifique se os Grupos de Segurança de Rede não estão restringindo o acesso de saída à Internet. Isso pode acontecer com as configurações de alguns Grupos de Segurança de Rede. Acesso de internet de saída (e DNS) é necessário para extensões de VM toobe migrados tooAzure Gerenciador de recursos. 
  - Há duas versões da saudação extensão BGInfo: v1 e v2.  Se Olá VM foi criada usando o portal clássico do hello ou o PowerShell, Olá VM provavelmente terão extensão de v1 Olá nele. Esta extensão não precisa toobe removida e será ignorada (não migrados) pela API de migração de saudação. No entanto, se Olá clássico VM foi criada com o novo portal do Azure de saudação, ela provavelmente terá Olá v2 com base em JSON versão de BGInfo, que pode ser migrado tooAzure Gerenciador de recursos fornecido agente hello está funcionando e se tem acesso de internet de saída (e DNS). 
  - **Opção de correção 1**. Se você souber que suas VMs não terá à internet de saída acessar um serviço DNS de trabalho e trabalhando agentes do Azure em VMs hello, desinstale todas as extensões VM como parte da migração de saudação antes de preparar, reinstale as extensões de VM Olá após a migração. 
  - **Opção de correção 2**. Se as extensões de VM são muito grandes de um obstáculo, outra opção é tooshutdown/desalocar todas as VMs antes da migração. Migrar Olá desalocada VMs e reiniciá-los na saudação do lado do Gerenciador de recursos do Azure. benefício de saudação aqui é que as extensões de VM serão migrados. Olá desvantagem é que todos os públicas de IPs virtuais serão perdidas (Isso pode ser um inicializador-não), e obviamente Olá VMs desligará causar um impacto muito maior em aplicativos de trabalho.

    > [!NOTE] 
    > Se uma política Central de segurança do Azure está configurada em relação a saudação sendo migradas de VMs em execução, política de segurança Olá precisa toobe interrompido antes de remover extensões, caso contrário segurança Olá extensão de monitoramento será reinstalado automaticamente Olá VM após removê-lo.

- **Conjuntos de disponibilidade** - para uma rede virtual (vNet) toobe migrados tooAzure Gerenciador de recursos, Olá VMs de implantação (ou seja, o serviço de nuvem) contida clássico deve ser em um conjunto de disponibilidade ou Olá VMs todos os não deve estar em qualquer conjunto de disponibilidade. Ter mais de um conjunto de disponibilidade no serviço de nuvem Olá não é compatível com o Gerenciador de recursos do Azure e interromperá a migração.  Além disso, não pode haver algumas VMs em um conjunto de disponibilidade e outras VMs que não estão em um conjunto de disponibilidade. tooresolve isso, você precisa tooremediate ou rearranjas essas seu serviço de nuvem.  Planeje de forma adequada, pois isso pode ser demorado. 

- **Implantações de função Web/trabalhador** -serviços de nuvem que contém funções web e de trabalho não é possível migrar tooAzure Gerenciador de recursos. funções de web/trabalho Olá devem ser removidas da rede virtual Olá antes de pode iniciar a migração.  Uma solução típica é toojust mover web/trabalhador função instâncias tooa clássico rede virtual separada que também é o circuito de rota expressa tooan vinculado ou toomigrate Olá código toonewer PaaS App Services (essa discussão está além do escopo deste documento hello). No primeiro Olá reimplantar caso, criar uma nova rede virtual do clássico, move/reimplantar Olá web/trabalhador funções toothat nova rede virtual e excluir as implantações de saudação da rede virtual do hello está sendo movido. Não é necessário alterar o código. Olá novo [emparelhamento de rede Virtual](../../virtual-network/virtual-network-peering-overview.md) recurso pode ser usado toopeer Olá juntos clássico rede virtual que contém funções de web/trabalho hello e outras redes virtuais no hello mesma região do Azure, como Olá rede virtual migrado (**após a migração da rede virtual como emparelhadas redes virtuais não podem ser migradas**), fornecendo, assim, Olá recursos mesmo sem perda de desempenho e penalidades nenhuma latência/largura de banda. Dada a adição de saudação do [emparelhamento de rede Virtual](../../virtual-network/virtual-network-peering-overview.md), implantações de função web/de trabalho agora pode ser facilmente reduzidas e não bloquear Olá migração tooAzure Gerenciador de recursos.

- **Cotas do Azure Resource Manager** – as regiões do Azure têm cotas/limites separados para o Clássico e o Azure Resource Manager. Mesmo que o novo hardware em um cenário de migração não está sendo consumido *(nós alternando VMs existentes do clássico tooAzure Gerenciador de recursos)*, as cotas do Azure Resource Manager ainda precisam toobe no local com capacidade suficiente antes pode começar a migração. Está listadas abaixo limites principais de saudação que vimos causam problemas.  Abra limita uma saudação tooraise de tíquete de suporte de cota. 

    > [!NOTE]
    > Esses limites necessário toobe gerado em Olá mesma região conforme migradas seu toobe ambiente atual.
    >

    - Interfaces de Rede
    - Balanceadores de Carga
    - IPs Públicos
    - IPs Públicos Estáticos
    - Núcleos
    - Grupos de segurança de rede
    - Tabelas de Rotas

    Você pode verificar suas cotas de Gerenciador de recursos do Azure atual usando Olá comandos com a versão mais recente de saudação do Azure CLI 2.0 a seguir.

    **Computação** *(Núcleos, Conjuntos de Disponibilidade)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **Rede** *(Redes Virtuais, IPs Públicos Estáticos, IPs Públicos, Grupos de Segurança de Rede, Interfaces de Rede, Balanceadores de Carga, Tabelas de Rotas)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **Armazenamento** *(Conta de Armazenamento)*
    
    ```bash
    az storage account show-usage
    ```

- **Limitação da API do Azure Resource Manager** – caso você tenha um ambiente grande o suficiente (por exemplo, > 400 VMs em uma rede virtual), você pode atingir o saudação padrão API limites para gravações de limitação (atualmente **1200 gravações por hora**) no Gerenciador de recursos do Azure. Antes de iniciar a migração, você deve gerar um tooincrease de tíquete de suporte a esse limite para sua assinatura.

- **Atingiu o tempo limite VM Status de provisionamento** - se uma VM tem o status de saudação do **de provisionamento esgotado**, este toobe necessidades resolvido antes da migração. Olá única forma toodo isso ocorre com tempo de inatividade por desprovisionamento/reprovisionamento Olá VM (delete, mantenha o disco hello e recrie Olá VM). 

- **Status da VM RoleStateUnknown** - se a migração é interrompida devido a tooa **estado da função desconhecido** erro mensagem, inspecionar Olá VM usando o portal de saudação e certifique-se de que ele está em execução. Esse erro normalmente desaparecerá por si só (sem nenhuma correção necessária) após alguns minutos e, em geral, é um tipo transitório que costuma ser observado durante as operações **start**, **stop** e **restart** de uma Máquina Virtual. **Melhor prática:** tente fazer a migração novamente após alguns minutos. 

- **O Fabric Cluster não existe** – em alguns casos, determinadas VMs não podem ser migradas por vários motivos incomuns. Um desses casos conhecidos é se hello VM tiver sido criado recentemente (em Olá última semana ou menos) e aconteceu tooland um cluster do Azure que ainda não está equipado para cargas de trabalho do Gerenciador de recursos do Azure.  Você obterá um erro que diz **não existe um cluster do fabric** e hello VM não pode ser migrada. Aguardar alguns dias geralmente resolverá esse problema específico como cluster Olá receberá em breve o Gerenciador de recursos do Azure habilitado. No entanto, uma solução imediata é muito`stop-deallocate` Olá VM, em seguida, continuar em frente com a migração de início, e Olá VM backup no Gerenciador de recursos do Azure após a migração.

### <a name="pitfalls-tooavoid"></a>Armadilhas tooavoid

- Não usar atalhos e omitir as migrações de simulação de validar/preparar/abort hello.
- A maioria, se não todas, de seus problemas potenciais serão superficial durante as etapas de validar/preparar/abort hello.

## <a name="migration"></a>Migração

### <a name="technical-considerations-and-tradeoffs"></a>Considerações técnicas e compensações

Agora você está pronto porque você trabalhou por meio de saudação problemas conhecidos com o seu ambiente.

Para migrações de saudação real, você pode desejar tooconsider:

1. Planejar e agendar a rede virtual hello (a menor unidade de migração) com o aumento de prioridade.  Olá simples redes virtuais pela primeira vez e andamento com hello mais complicado redes virtuais.
2. A maioria dos clientes terá ambientes de produção e de não produção.  Agendar a produção por último.
3. **(OPCIONAL)** Agendar um tempo de inatividade de manutenção com uma grande quantidade de buffer caso ocorram problemas inesperados.
4. Comunicar-se e alinhar com as equipes de suporte em caso de problemas.

### <a name="patterns-of-success"></a>Padrões de sucesso

orientação técnica de saudação do hello acima da seção de teste de laboratório deve ser considerada e atenuados migração real tooa anterior.  Com os testes adequados, a migração de saudação é, na verdade, um evento diferente.  Para ambientes de produção, talvez seja útil toohave adicionais de suporte, como um parceiro confiável da Microsoft ou serviços Microsoft Premier.

### <a name="pitfalls-tooavoid"></a>Armadilhas tooavoid

Testes não totalmente podem causar problemas e atraso na migração de saudação.  

## <a name="beyond-migration"></a>Além da migração

### <a name="technical-considerations-and-tradeoffs"></a>Considerações técnicas e compensações

Agora que você está no Gerenciador de recursos do Azure, maximize a plataforma de saudação.  Saudação de leitura [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md) toofind out sobre os benefícios adicionais.

Tooconsider coisas:

- Agrupamento de migração de saudação com outras atividades.  A maioria dos clientes opta por uma janela de manutenção do aplicativo.  Se assim, talvez você queira toouse tooenable esse tempo de inatividade outros recursos do Azure Resource Manager, como criptografia e migração tooManaged discos.
- Rever Olá técnica e motivos dos negócios para o Azure Resource Manager; Habilite Olá serviços adicionais disponíveis somente no Azure Resource Manager que se aplicam a tooyour ambiente.
- Modernize seu ambiente com os serviços de PaaS.

### <a name="patterns-of-success"></a>Padrões de sucesso

Ser proposital em quais serviços você agora deseja tooenable no Gerenciador de recursos do Azure.  Muitos clientes encontrar hello abaixo convincente para seus ambientes do Azure:

- [Controle de Acesso Baseado em Função](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Modelos do Azure Resource Manager para uma implantação mais fácil e mais controlada](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Marcas](../../azure-resource-manager/resource-group-using-tags.md).
- [Controle de Atividades](../../azure-resource-manager/resource-group-audit.md)
- [Políticas de Recursos](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Armadilhas tooavoid

Lembre-se de por que você iniciou este jornada de migração do Gerenciador de recursos de tooAzure clássico.  Quais são os motivos dos negócios Olá original? Você atingiu motivo de negócios Olá?


## <a name="next-steps"></a>Próximas etapas

* [Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
