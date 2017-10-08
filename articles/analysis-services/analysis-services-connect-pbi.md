---
title: aaaConnect tooAzure Analysis Services com o Power BI | Microsoft Docs
description: Saiba como tooconnect tooan Azure Analysis Services server usando o Power BI.
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Conectar com Power BI

Depois que você criou um servidor no Azure e implantou um modelo de tabela tooit, os usuários em sua organização são tooconnect pronto e começam a explorar os dados. 

> [!TIP]
> Ter a versão mais recente do se Olá de toouse de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Conexão no Power BI Desktop

1. No Power BI Desktop, clique em **Obter Dados** > **Azure** > **Banco de dados do Azure Analysis Services**.

2. Em **servidor**, digite o nome do servidor de saudação. 
    
    Ser se tooinclude Olá a URL completa. Por exemplo, asazure://westcentralus.asazure.windows.net/advworks.

3. Em **banco de dados**, se você souber o nome de saudação do banco de dados de modelo de tabela Olá ou perspectiva que você deseja tooconnect para, cole-o aqui. Caso contrário, você pode deixar esse campo em branco e selecionar um banco de dados ou perspectiva posteriormente.

4. Deixe o padrão de saudação **conectar-se ao vivo** opção e, em seguida, pressione **conectar**. 

5. Se solicitado, insira suas credenciais de logon. 

6. Em **navegador**, expanda o servidor de saudação e selecione o modelo hello ou perspectiva que você deseja tooconnect para, em seguida, clique em **conectar**. Clique em um modelo ou perspectiva tooshow todos os objetos de saudação para esse modo de exibição.

    modelo de saudação é aberto no Power BI Desktop com um relatório em branco na exibição de relatório. lista de campos de saudação exibe todos os objetos de modelo não ocultos. Status da Conexão é exibido no canto inferior direito de saudação.

## <a name="connect-in-power-bi-service"></a>Conectar-se no Power BI (serviço)

1. Crie um arquivo de área de trabalho do Power BI com um modelo de tooyour de conexão ao vivo em seu servidor.
2. No [Power BI](https://powerbi.microsoft.com), clique em **Obter Dados** > **Arquivos**. Localize e selecione o arquivo.



## <a name="see-also"></a>Consulte também
[Conecte-se tooAzure Analysis Services](analysis-services-connect.md)   
[Bibliotecas de cliente](analysis-services-data-providers.md)

