---
title: "aaaCreate exibições tooanalyze dados na análise de Log do OMS | Microsoft Docs"
description: "Designer de exibição na análise de Log permite que você toocreate personalizado exibições que são exibidas no portal do OMS e o Azure hello e contêm diferentes visualizações de dados no repositório do OMS hello. Este artigo contém uma visão geral do Designer de modos de exibição e dos procedimentos para criar e editar exibições personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Usar exibições personalizadas do Designer de exibição toocreate na análise de Log
Olá Designer de exibição no [análise de Log](log-analytics-overview.md) permite que você toocreate modos de exibição personalizados no console do OMS Olá que contêm diferentes visualizações de dados no repositório do OMS hello. Este artigo contém uma visão geral do Designer de modos de exibição e dos procedimentos para criar e editar exibições personalizadas.

Outros artigos disponíveis para o Designer de modo de exibição:

* [Referência de bloco](log-analytics-view-designer-tiles.md) -referência de configurações de saudação de cada Olá blocos toouse disponível em exibições personalizadas.
* [Referência de parte da visualização](log-analytics-view-designer-parts.md) -referência de configurações de saudação de cada Olá blocos toouse disponível em exibições personalizadas.

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), consultas em todos os modos de exibição devem ser gravada em Olá [nova linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas as exibições que foram criadas antes de atualizar o espaço de trabalho de saudação será automtically convertido.

## <a name="concepts"></a>Conceitos
Exibições criadas com hello Designer de exibição contém elementos Olá Olá a tabela a seguir.

| Parte | Descrição |
|:--- |:--- |
| Bloco |Exibido no painel de visão geral de análise de Log principal hello.  Inclui um resumo visual de informações de saudação contida no hello exibição personalizada.  Diferentes tipos de bloco fornecem visualizações diferentes de registros no repositório do OMS hello.  Clique em Olá Olá tooopen de bloco de exibição personalizado. |
| Exibição personalizada |Exibida quando o usuário Olá clica em Olá lado a lado.  Contém uma ou mais partes da visualização. |
| Partes da visualização |Visualização de dados no repositório do OMS Olá com base em um ou mais [pesquisas de log](log-analytics-log-searches.md).  A maioria das partes incluirá um cabeçalho que fornece uma visualização de alto nível e uma lista dos primeiros resultados de saudação.  Tipos de outra parte fornecem visualizações diferentes de registros no repositório do OMS hello.  Clique em elementos Olá parte tooperform uma pesquisa de log fornecendo registros detalhados. |

![Visão geral do Designer de modo de exibição](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Adicionar espaço de trabalho do Designer de exibição tooyour
Enquanto o Designer de exibição está em visualização, você deve adicioná-lo tooyour espaço de trabalho selecionando **recursos de visualização** em Olá **configurações** seção do portal do OMS hello.

![Habilitar visualização](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Criar e editar modos de exibição
### <a name="create-a-new-view"></a>Criar um novo modo de exibição
Abra uma nova exibição no hello **Designer de exibição** clicando em Olá Designer de exibição lado a lado no painel principal de OMS hello.

![Bloco Designer de modo de exibição](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Editar um modo de exibição existente
tooedit uma exibição existente no hello Designer de exibição, abrir Olá exibição clicando no seu bloco no painel principal de OMS hello.  Em seguida, clique em Olá **editar** botão tooopen Olá exibição no hello Designer de exibição.

![Editar um modo de exibição](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Clonar um modo de exibição existente
Quando você clona um modo de exibição, ele cria uma nova exibição e abre em Olá Designer de exibição.  nova exibição da saudação terá Olá mesmo nome como Olá original com "Cópia" anexado toohello final.  tooclone uma exibição, modo de exibição existente clicando no seu bloco no painel principal de OMS Olá Olá aberto.  Em seguida, clique em Olá **Clone** botão tooopen Olá exibição no hello Designer de exibição.

![Clonar um modo de exibição](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Excluir um modo de exibição existente
toodelete uma exibição existente, Olá Abrir exibição clicando no seu bloco no painel principal de OMS hello.  Em seguida, clique em Olá **editar** botão tooopen Olá exibição no hello Designer de exibição e, em seguida, clique em **Excluir modo de exibição**.

![Excluir um modo de exibição](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Exportar um modo de exibição existente
Você pode exportar um arquivo JSON tooa de modo que você pode importar para outro espaço de trabalho ou use um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport uma exibição existente, Olá Abrir exibição clicando no seu bloco no painel principal de OMS hello.  Em seguida, clique em Olá **exportar** botão toocreate um arquivo na pasta de download do navegador hello.  nome de saudação do arquivo hello será o nome de saudação do modo de exibição de saudação com extensão Olá *omsview*.

![Exportar um modo de exibição](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importar um modo de exibição existente
Você pode importar um arquivo *omsview* exportado de outro grupo de gerenciamento.  tooimport uma exibição existente, primeiro crie uma nova exibição.  Em seguida, clique em Olá **importação** botão e selecione Olá *omsview* arquivo.  configuração Olá no arquivo hello será copiada para o modo de exibição existente hello.

![Exportar um modo de exibição](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Trabalhando com o Designer de modo de exibição
Olá Designer de exibição tem três painéis.  Olá **Design** painel representa o modo de exibição personalizado hello.  Quando você adiciona os blocos e partes de saudação **controle** painel toohello **Design** painel forem adicionados toohello exibição.  Olá **propriedades** painel exibirá propriedades de saudação de bloco de saudação ou a parte selecionada.

![Criador de Modos de Exibição](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Configurar bloco de modo de exibição
Um modo de exibição personalizado pode ter apenas um único bloco.  Selecione Olá **bloco** guia Olá **controle** painel tooview Olá atual lado a lado ou selecione um alternativo.  Olá **propriedades** painel exibirá propriedades de saudação de bloco atual hello.  Configurar propriedades de bloco Olá toohello de acordo com informações detalhadas em Olá [referência bloco](log-analytics-view-designer-tiles.md) e clique em **aplicar** toosave alterações.

### <a name="configure-visualization-parts"></a>Configurar partes da visualização
Um modo de exibição pode incluir qualquer número de partes de visualização.  Selecione Olá **exibição** tooadd toohello exibição de parte de guia e, em seguida, uma visualização.  Olá **propriedades** painel exibirá propriedades Olá para parte de saudação selecionada.  Configurar modo de exibição de saudação propriedades toohello de acordo com informações detalhadas em Olá [referência de parte da visualização](log-analytics-view-designer-parts.md) e clique em **aplicar** toosave alterações.

### <a name="delete-a-visualization-part"></a>Excluir uma parte da visualização
Você pode remover uma parte da visualização da exibição de saudação clicando Olá **X** botão no canto superior direito de saudação da parte de saudação.

### <a name="rearrange-visualization-parts"></a>Reorganizar partes de visualização
Os modos de exibição têm apenas uma linha de partes da visualização.  Reorganize partes existentes em uma exibição clicando e arrastando-os tooa novo local.

## <a name="next-steps"></a>Próximas etapas
* Adicionar [blocos](log-analytics-view-designer-tiles.md) tooyour modo de exibição personalizado.
* Adicionar [visualização partes](log-analytics-view-designer-parts.md) tooyour modo de exibição personalizado.
