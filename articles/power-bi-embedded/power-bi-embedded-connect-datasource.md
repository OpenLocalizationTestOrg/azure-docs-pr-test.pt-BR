---
title: aaaMicrosoft Power BI inserido - conectar fonte de dados tooa
description: Power BI inserido, conecte-se a fontes de toodata
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Conecte-se a fonte de dados tooa
Com o **Power BI Embedded**, você pode inserir relatórios em seu próprio aplicativo. Quando você insere um relatório do Power BI em seu aplicativo, o relatório de saudação se conecta toohello base de dados por **importando** uma cópia dos dados de saudação ou por **conectando diretamente** toohello fonte de dados usando  **DirectQuery**.

Aqui estão Olá diferenças entre usar **importação** e **DirectQuery**.

| Importar | DirectQuery |
| --- | --- |
| Tabelas, colunas, *e dados* são importados ou copiados para o conjunto de dados do relatório hello. toosee altera os dados subjacentes toohello ocorreu, você deve atualizar ou importar novamente um dataset completo e atual. |Somente *tabelas e colunas* são importados ou copiados para o conjunto de dados do relatório hello. Você sempre pode exibir dados mais atuais da saudação. |

Com o Power BI Embedded, você pode usar DirectQuery com fontes de dados de nuvem, mas não em fontes de dados locais no momento.

> [!NOTE]
> Olá Gateway de dados no local não é suportado com o Power BI inserido no momento. Isso significa que não é possível usar o DirectQuery com fontes de dados locais.

## <a name="supported-data-sources"></a>Fontes de dados com suporte

**DirectQuery**
* Banco de Dados SQL Azure
* SQL Data Warehouse do Azure

**Importaçãoação**

Você pode importar usando todas as fontes de dados disponíveis Olá no Power BI Desktop. Você vai **não** ser capaz de toorefresh esses dados no Power BI inserido. Você terá as alterações de tooupload tooyour PBIX arquivo tooPower BI inserido. Isso é devido gateway disponível toono. 

## <a name="benefits-of-using-directquery"></a>Benefícios do uso do DirectQuery
Há duas vantagens principais ao usar **DirectQuery**:

* **DirectQuery** Olá de permite que você cria visualizações de conjuntos de dados muito grandes, onde caso contrário, seria impraticável toofirst importar todos os dados.
* Alterações de dados subjacentes podem exigir uma atualização de dados e para alguns relatórios, hello precisam de dados atuais toodisplay pode exigir transferências de dados grandes, tornando os dados de reimportação impraticável. Por outro lado, relatórios do **DirectQuery** sempre usam dados atuais.

## <a name="limitations-of-directquery"></a>Limitações do DirectQuery
   Há alguns toousing de limitações **DirectQuery**:

* Todas as tabelas devem vir de um banco de dados individual.
* Se a consulta de saudação for excessivamente complexa, ocorrerá um erro. Erro de saudação tooremedy deve refatorar consulta Olá é menos complexo. Se Olá consulta deve ser complexa, você terá dados de saudação tooimport em vez de usar **DirectQuery**.
* A filtragem de relação é limitada tooa única direção, em vez de ambas as direções.
* Não é possível alterar o tipo de dados de saudação de uma coluna.
* Por padrão, as limitações são colocadas em expressões DAX permitidas em medidas. Consulte [DirectQuery e medidas](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery e medidas
consultas de tooensure enviadas toohello fonte de dados têm um desempenho aceitável, são impostas limitações às medidas. Ao usar **Power BI Desktop**avançado os usuários podem escolher essa limitação de toobypass escolhendo **arquivo > Opções e configurações > Opções**. Em Olá **opções** caixa de diálogo, escolha **DirectQuery**e selecione a opção de saudação **permitir medidas irrestritas no modo DirectQuery**. Quando essa opção estiver selecionada, qualquer expressão DAX válida para uma determinada medida poderá ser usada. Os usuários devem estar cientes; No entanto, que algumas expressões que funcionam muito bem quando os dados de saudação são importados pode resultar em consultas muito lentas toohello backend de origem no **DirectQuery** modo. 

## <a name="see-also"></a>Consulte também
* [Introdução ao Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

