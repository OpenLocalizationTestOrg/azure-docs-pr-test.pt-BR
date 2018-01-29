---
title: Conectar-se ao Azure Analysis Services com Power BI | Microsoft Docs
description: Saiba como se conectar a um servidor Azure Analysis Services usando Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/10/2018
ms.author: owend
ms.openlocfilehash: ea1094d0ce858cd7df9c49f18fb81b07e31fca53
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2018
---
# <a name="connect-with-power-bi"></a>Conectar com Power BI

Depois de criar um servidor no Azure e implantar um modelo tabular nele, os usuários em sua organização estarão prontos para se conectar e começar a explorar os dados. 

> [!TIP]
> Certifique-se de usar a versão mais recente do [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Conexão no Power BI Desktop

1. No Power BI Desktop, clique em **Obter Dados** > **Azure** > **Banco de dados do Azure Analysis Services**.

2. Em **Servidor**, insira o nome do servidor. Certifique-se de incluir a URL completa, por exemplo, asazure://westcentralus.asazure.windows.net/advworks.

3. Em **Banco de Dados**, se você souber o nome do banco de dados de modelo de tabela ou da perspectiva a qual você deseja se conectar, cole-o aqui. Caso contrário, você pode deixar esse campo em branco e selecionar um banco de dados ou perspectiva posteriormente.

4. Deixe a opção **Conectar em tempo real** padrão selecionada e, em seguida, pressione **Conectar**. Atualmente não há suporte para importar conexões.

5. Se solicitado, insira suas credenciais de logon. 

6. Em **Navegador**, expanda o servidor e selecione o modelo ou a perspectiva a qual você deseja se conectar e clique em **Conectar**. Clique em um modelo ou perspectiva para exibir todos os objetos dessa visualização.

    O modelo é aberto no Power BI Desktop com um relatório em branco na exibição de Relatório. A lista de Campos exibe todos os objetos modelo não ocultos. O status de conexão é exibido no canto inferior direito.

## <a name="connect-in-power-bi-service"></a>Conectar-se no Power BI (serviço)

1. Crie um arquivo do Power BI Desktop que tenha uma conexão ativa com seu modelo no servidor.
2. Em [Power BI](https://powerbi.microsoft.com), clique em **Obter Dados** > **Arquivos**, e, em seguida, localize e selecione o arquivo. pbix.



## <a name="see-also"></a>Consulte também
[Conectar-se ao Azure Analysis Services](analysis-services-connect.md)   
[Bibliotecas de cliente](analysis-services-data-providers.md)

