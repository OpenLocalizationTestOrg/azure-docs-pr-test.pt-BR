---
title: "custos de aaaManage efetivamente para SQL Server em máquinas virtuais do Azure | Microsoft Docs"
description: "Fornece as práticas recomendadas para a escolha de saudação à direita do SQL Server máquina virtual modelo de preços."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Diretrizes de preços para VMs do Azure do SQL Server

Este tópico fornece diretrizes de preços para máquinas virtuais do SQL Server no Azure. Há várias opções que afetam o custo, e é importante toopick Olá imagem à direita que Equilibre os custos com requisitos de negócios.

## <a name="free-licensed-sql-server-editions"></a>Edições do SQL Server com licença gratuita

Se você quiser toodevelop, testar, ou criar uma prova de conceito, use Olá licenciado livre **edição do SQL Server Developer**. Esta edição tem tudo no SQL Server Enterprise edition, assim, você pode usá-lo toobuild qualquer aplicativo que você deseja. Não é permitido toorun em produção. Uma VM do SQL Server Developer cobrará somente para custo Olá Olá VM, não para licenciamento do SQL Server.

Se você quiser toorun uma carga de trabalho leve em produção (< 4 núcleos, < 1 GB de memória, < 10 GB/banco de dados), use Olá licenciado livre **SQL Server Express edition**. Uma VM do SQL Express somente cobrará custo de saudação da saudação VM, não licenciamento do SQL.

Para essas cargas de trabalho de produção leve ou desenvolvimento/teste, você também poderá economizar escolhendo uma VM menor que corresponda a essas cargas de trabalho. Olá DS1v2 pode ser uma boa escolha para essas cargas de trabalho.

toocreate uma VM do Azure SQL Server 2016 com uma dessas imagens, consulte Olá links a seguir:

- [VM do Azure do SQL Server 2016 Developer](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [VM do Azure do SQL Server 2016 Express](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Edições pagas do SQL Server

Se você tiver uma carga de trabalho de produção não leve, use um dos Olá edições do SQL Server a seguir:

| Edição do SQL Server | Carga de trabalho |
|-----|-----|
| Web | Sites pequenos |
| Standard | Toomedium pequenas cargas de trabalho |
| Enterprise | Cargas de trabalho grandes ou críticas|

Você tem dois toopay de opções de licenciamento do SQL Server para estas edições: *pagamento por uso* ou *Traga sua própria licença*.

### <a name="pay-per-usage"></a>Pagamento por uso

**Licença do SQL Server Olá pagamento por uso** significa que o custo por minuto Olá executando Olá VM do Azure contém o custo de saudação de licença do SQL Server hello. Você pode ver o hello preços para edições do SQL Server diferentes hello (Web, Standard, Enterprise) no hello [página de preços de VM do Azure](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Olá custo é hello mesmo para todas as versões do SQL Server (2008 R2 too2016). Como com o SQL Server em geral, licenciamento Olá o custo de licenciamento por minuto depende Olá número de núcleos VM.

Pagar saudação do SQL Server por uso de licenciamento é recomendado para:

- Cargas de trabalho temporárias ou periódicas. Por exemplo, um aplicativo que precisa toosupport um evento para alguns meses cada ano ou a análise de negócios às segundas-feiras.
- Cargas de trabalho com tempo de vida ou escala desconhecidos. Por exemplo, um aplicativo que pode não ser necessário por alguns meses, ou que pode exigir mais, ou menos capacidade de computação, dependendo da demanda.

toocreate uma VM do Azure SQL Server 2016 com uma dessas imagens de pagamento por uso, consulte Olá links a seguir:

- [VM do Azure do SQL Server 2016 Web](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [VM do Azure do SQL Server 2016 Standard](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [VM do Azure do SQL Server 2016 Enterprise](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Quando você cria uma máquina virtual SQL Server no hello portal do Azure, Olá estimado custo mensal, exibido em Olá **escolher um tamanho** folha não inclui os custos de licenciamento do SQL Server. Esse é o custo de saudação do hello VM autônoma.
>
> ![Folha Escolher tamanho da VM](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Olá licenciado livre Express e o desenvolvedor nas edições do SQL Server, isso é o custo estimado total hello. Mas para Enterprise, Standard e Web, localize Olá adicionais custos de licenciamento do SQL em Olá [página de preços máquinas virtuais do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Na página de preços de hello, selecione sua edição do destino do SQL Server.

### <a name="bring-your-own-license-byol"></a>BYOL (Traga sua própria licença)

**Colocar sua própria licença do SQL Server por meio de mobilidade de licença**, também chamado tooas **BYOL**, significa usando uma licença de Volume existente do SQL Server com o Software Assurance em uma VM do Azure. Uma VM do SQL Server usando BYOL cobrará somente para custo de saudação da execução Olá VM, não para o licenciamento do SQL Server, considerando que você já tiver adquirido licenças e Software Assurance através de um programa de licenciamento por Volume.

Trazer seu próprio licenciamento do SQL por meio da Mobilidade de Licença é recomendável para:

- Cargas de trabalho contínuas. Por exemplo, um aplicativo que precisa de operações de negócios toosupport 24x7.
- Cargas de trabalho com tempo de vida e escala conhecidos. Por exemplo, um aplicativo que será necessário para o ano inteiro hello e quais demanda foi prevista.

toouse BYOL com uma VM do SQL Server, você deve ter uma licença para o SQL Server Standard ou Enterprise e [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), que é uma opção necessária por algumas [licenciamento por Volume](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programas e opcional comprar com outras pessoas.  Olá níveis fornecidos por meio de programas de licenciamento por Volume de preço varia de acordo com base no tipo de saudação do contrato e hello quantidade e ou compromisso tooSQL Server. Mas como regra geral, para trazer sua própria licença por cargas de trabalho de produção contínuo tem Olá benefícios a seguir:

| Benefício do método BYOL | Descrição |
|-----|-----|
| **Economia de custos** | Trazer usa própria licença do SQL Server é mais econômico do que pagar pelo uso se uma carga de trabalho for executar continuamente o SQL Server Standard ou Enterprise por *mais de 10 meses*. |
| **Economias de longo prazo** | Em média, ele é *30% mais barato por ano* toobuy ou renovar uma licença do SQL Server para Olá primeiro 3 anos. Além disso, após 3 anos, você não precisa toorenew Olá licença, pagamento apenas para Software Assurance. Nesse ponto, *a economia é de 200%*. |
| **Réplica secundária passiva gratuita** | Outro benefício de trazer sua própria licença é hello [livre de licenciamento para uma réplica secundária passiva](https://azure.microsoft.com/pricing/licensing-faq/) por SQL Server para fins de alta disponibilidade. Isso reduz o hello metade licenciamento custo de uma implantação do SQL Server altamente disponível (por exemplo, usando grupos de disponibilidade AlwaysOn). secundário passivo do Olá Olá direitos toorun são fornecidos pelo Olá benefício failover servidores Software Assurance. |

toocreate uma VM do Azure SQL Server 2016 com uma dessas imagens colocar seu-proprietário-licenças, consulte VMs Olá prefixadas com "{BYOL}":

- [VM do Azure do SQL Server 2016 Enterprise](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [VM do Azure do SQL Server 2016 Standard](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Informe-nos em até 10 dias quantas licenças do SQL Server você usará no Azure. Olá links toohello anterior imagens têm instruções sobre como toodo isso.

## <a name="avoid-unecessary-costs"></a>Evitar custos desnecessários

Se você estiver usando qualquer cargas de trabalho que não são executados continuamente, considere a possibilidade de desligar a máquina de virtual de saudação durante períodos de saudação inativo. Você paga apenas pelo que usa.

Por exemplo, se você estiver tentando simplesmente SQL Server em uma VM do Azure, não seria conveniente tooincur encargos, deixando-o em execução por semanas acidentalmente. Uma solução é Olá toouse [recurso desligamento automático](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Desligamento automático da VM do SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

O desligamento automático faz parte de um conjunto maior de recursos semelhantes fornecido pelo [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Para outros fluxos de trabalho, considere o desligamento e a reinicialização automáticos das VMs do Azure com uma solução por script, como a [Automação do Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Desligar e desalocar sua VM são únicas cobranças de tooavoid de maneira hello. Simplesmente parada ou usando tooshut de opções de energia para baixo Olá VM ainda incorrerá em encargos de uso.

## <a name="next-steps"></a>Próximas etapas

Para obter diretrizes gerais de preços do Azure, confira [Evitar custos inesperados com o gerenciamento de custo e cobrança do Azure](../../../billing/billing-getting-started.md).

Para Olá máquinas virtuais mais recente do preço, incluindo o SQL Server, consulte Olá [página de preços de VM do Azure](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Examine outros tópicos sobre Máquinas Virtuais do SQL Server em [Visão geral do SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).
