---
title: aaaConnect tooAzure Analysis Services com o Excel | Microsoft Docs
description: Saiba como tooconnect tooan Azure Analysis Services server usando o Excel.
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Conectar com o Excel

Depois que você criou um servidor no Azure e implantou um modelo de tabela tooit, você está pronto tooconnect e começar a explorar os dados.


## <a name="connect-in-excel"></a>Conectar-se no Excel

Há suporte para a conexão de servidor tooa no Excel usando obter dados no Excel 2016. Não há suporte para a conexão usando Olá Assistente de importação de tabela no Power Pivot. 

**tooconnect no Excel 2016**

1. No Excel 2016, Olá **dados** de faixa de opções, clique em **obter dados externos** > **de outras fontes** > **do Analysis Services** .

2. Em Olá Assistente de Conexão de dados, em **nome do servidor**, digite nome do servidor de saudação incluindo protocolo e URI. Em seguida, em **credenciais de Logon**, selecione **Olá usar nome de usuário e senha a seguir**e digite o nome de usuário da organização hello, por exemplo nancy@adventureworks.come a senha.

    ![Conectar a partir do logon do Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. Em **Selecionar banco de dados e tabela**, selecione o banco de dados de saudação e o modelo ou perspectiva e, em seguida, clique em **concluir**.
   
    ![Conectar a partir do modelo de seleção do Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Consulte também
[Bibliotecas do cliente](analysis-services-data-providers.md)   
[Gerenciar seu serviço](analysis-services-manage.md)     


