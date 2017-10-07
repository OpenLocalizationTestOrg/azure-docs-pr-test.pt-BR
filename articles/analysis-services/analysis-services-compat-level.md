---
title: "nível de compatibilidade de modelo aaaData no Azure Analysis Services | Microsoft Docs"
description: "Noções básicas sobre o nível de compatibilidade do modelo de dados de tabela."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nível de compatibilidade para modelos de tabela do Analysis Services

*Nível de compatibilidade* refere-se comportamentos específicos toorelease no mecanismo do Analysis Services hello. Nível de compatibilidade de toohello alterações geralmente coincidam com as versões principais do SQL Server. Essas alterações também são implementadas no paridade do Azure Analysis Services toomaintain entre as duas plataformas. Alterações de nível de compatibilidade também afetam os recursos disponíveis em modelos de tabela. Por exemplo, o DirectQuery e os metadados de objeto de tabela têm implementações diferentes dependendo do nível de compatibilidade de saudação. 

Serviços de análise do Azure oferece suporte a modelos de tabela em níveis de compatibilidade Olá 1200 e 1400.

o nível de compatibilidade mais recente Olá é 1400. Esse nível coincide com o Analysis Services do SQL Server 2017. Os principais recursos no nível de compatibilidade de 1400 Olá incluem:

*  Nova infraestrutura para conectividade de dados e importação para modelos de tabela com suporte para APIs de TOM e scripts de TMSL. Esse novo recurso habilita o suporte para fontes de dados adicionais, como armazenamento de Blobs do Azure.
*  Transformação de dados e recursos de mashup de dados usando expressões Obter dados e M.
*  Medidas que suportam uma propriedade de linhas de detalhes com uma expressão DAX. Essa propriedade permite que as ferramentas de cliente como o Microsoft Excel toodrill toodetailed dados de um relatório agregado. Por exemplo, quando os usuários exibem o total de vendas de uma região e mês, eles podem exibir detalhes do pedido Olá associado. 
*  Segurança em nível de objeto de tabela e coluna nomes, além de toohello dados dentro deles.
*  Suporte aprimorado para hierarquias desbalanceadas.
*  Monitoramento de desempenho e melhorias.
  
## <a name="set-compatibility-level"></a>Configuração de nível de compatibilidade 
 Ao criar um novo projeto de modelo de tabela no SSDT, você pode especificar o nível de compatibilidade de saudação em Olá **designer de modelo Tabular** caixa de diálogo. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Se você selecionar Olá **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes usam o nível de compatibilidade Olá especificado como o padrão de saudação. Você pode alterar o nível de compatibilidade saudação padrão no SSDT em **ferramentas** > **opções**.  
  
 tooupgrade um projeto de modelo de tabela existente no SSDT, Olá conjunto **nível de compatibilidade** propriedade modelo Olá **propriedades** janela. Tenha em mente, atualizar o nível de compatibilidade Olá é irreversível.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Verifique o nível de compatibilidade de um banco de dados de modelo de tabela no SQL Server Management Studio 
 No SSMS, clique no nome do banco de dados hello > **propriedades** > **nível de compatibilidade**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Verifique o nível de compatibilidade com suporte para um servidor no SSMS  
 No SSMS, clique no nome do servidor de saudação > **propriedades** > **nível de compatibilidade com suporte**.  
  
 Essa propriedade especifica hello mais alto nível de compatibilidade de um banco de dados que serão executados no servidor de saudação (excluindo a visualização). Olá suporte para nível de compatibilidade não pode ser alterado.  

## <a name="next-steps"></a>Próximas etapas
  [Como criar um modelo no portal do Azure](analysis-services-create-model-portal.md)   
  [Gerenciar o Analysis Services](analysis-services-manage.md)  
