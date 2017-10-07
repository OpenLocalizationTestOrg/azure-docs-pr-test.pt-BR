---
title: "aaaEnable automático de ajuste de banco de dados do SQL Azure | Microsoft Docs"
description: "Habilite o ajuste automático do Banco de Dados SQL do Azure com facilidade."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Habilitar o ajuste automático

Banco de dados do SQL Azure é um serviço de dados gerenciados automaticamente que constantemente monitora suas consultas e identifica Olá ação que você pode realizar tooimprove o desempenho da carga de trabalho. Examine as recomendações e aplique-as manualmente ou permita que o Banco de Dados SQL do Azure aplique as ações corretivas automaticamente – isso é conhecido como **modo de ajuste automático**. Ajuste automático pode ser habilitado no servidor de saudação ou nível de banco de dados de saudação.

## <a name="enable-automatic-tuning-on-server"></a>Habilitar o ajuste automático no servidor

tooenable automático de ajuste no servidor de banco de dados SQL, navegar toohello server no Azure portal e, em seguida, selecione **ajuste automático** no menu de saudação. Selecione Olá opções de ajuste automático, você deseja tooenable e selecione **aplicar**:

![Servidor](./media/sql-database-automatic-tuning-enable/server.png)

Automáticos de opções no servidor de ajuste são aplicadas tooall bancos de dados no servidor de saudação. Por padrão, todos os bancos de dados herdam a configuração de saudação do seu servidor pai, mas isso pode ser substituído e especificado individualmente para cada banco de dados.

## <a name="configure-automatic-tuning-on-database"></a>Configurar o ajuste automático no banco de dados

Hello Azure portal permite que você tooindividually especificar a configuração de ajuste automático de saudação em cada banco de dados.

> [!NOTE]
> recomendação geral Olá é toomanage Olá ajuste a configuração automática no nível do servidor caso Olá mesmas definições de configuração podem ser aplicadas em cada banco de dados automaticamente. Configure o ajuste automático em um banco de dados individual se a diferente que outras pessoas na Olá mesmo servidor do banco de dados de saudação.
>

tooenable automático de ajuste em um único banco de dados, navegue toohello banco de dados em Olá portal do Azure e, em seguida e selecione **ajuste automático**. Você pode configurar um único banco de dados tooinherit saudação do banco de dados de saudação selecionando a caixa de seleção hello, ou você pode especificar a configuração de saudação para um banco de dados individualmente.

![Banco de dados](./media/sql-database-automatic-tuning-enable/database.png)

Depois de selecionar a configuração apropriada, clique em **Aplicar**.

## <a name="next-steps"></a>Próximas etapas
* Saudação de leitura [artigo ajuste automático](sql-database-automatic-tuning.md) toolearn mais informações sobre o ajuste automático e como ele pode ajudar a melhorar o desempenho.
* Consulte [Recomendações de desempenho](sql-database-advisor.md) para obter uma visão geral das recomendações de desempenho do Banco de Dados SQL do Azure.
* Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre como exibir o impacto no desempenho Olá as consultas principais.
