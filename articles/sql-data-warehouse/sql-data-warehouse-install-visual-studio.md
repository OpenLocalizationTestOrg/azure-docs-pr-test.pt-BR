---
title: aaaInstall Visual Studio e SSDT para SQL Data Warehouse | Microsoft Docs
description: Instalar o Visual Studio e o SSDT (Ferramentas de Desenvolvimento do SQL Server) para o SQL Data Warehouse do Azure
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Instalar o Visual Studio e o SSDT para o SQL Data Warehouse
toodevelop aplicativos para o SQL Data Warehouse, é recomendável usar a versão mais recente de saudação do Visual Studio com a versão mais recente de saudação do SQL Server Data Tools (SSDT).  Também há suporte para o Visual Studio 2013 Atualização 5 com SSDT a fim de permitir a compatibilidade com versões anteriores.  

Usando o Visual Studio com o SSDT permitirá toouse Olá Pesquisador de objetos do SQL Server toovisually explorar as tabelas, exibições, procedimentos armazenados e muito mais objetos no SQL Data Warehouse, bem como executar consultas.

> [!NOTE]
> O SQL Data Warehouse ainda não dá suporte aos Projetos do Banco de Dados do Visual Studio.  Este recurso será adicionado em uma futura versão.
> 
> 

## <a name="step-1-install-visual-studio"></a>Etapa 1: instalar o Visual Studio
Siga essas toodownload links e instalar o Visual Studio. Se você já tiver o Visual Studio 2013 ou posterior instalado, você pode ignorar tooStep 2, instale o SSDT.

1. [Baixar o Visual Studio][].
2. Siga Olá [instalar o Visual Studio] [ Installing Visual Studio] guia no MSDN e escolha as configurações padrão de saudação.

## <a name="step-2-install-ssdt"></a>Etapa 2: Instalar o SSDT
Basta marcar tooinstall SSDT para Visual Studio para uma atualização do SSDT de dentro do Visual Studio seguindo estas etapas.

1. No Visual Studio, clique em **Ferramentas** / **Extensões e Atualizações…** / **Atualizações**
2. Selecione **Atualizações do Produto**, em seguida, procure **Atualização do Microsoft SQL Server para as ferramentas do banco de dados**

Se uma atualização não for encontrada, você deve ter versão mais recente do hello instalada.  tooconfirm SSDT está instalado, clique em **ajuda** / **sobre o Microsoft Visual Studio** e procure por ferramentas de dados do SQL Server na lista de saudação.  versão mais recente de saudação do SSDT é 14.0.60525.0.  Se Olá opção tooinstall não está disponível no Visual Studio, como alternativa você pode visitar Olá [de Download do SSDT] [ SSDT Download] página toodownload e instalar o SSDT manualmente.

## <a name="next-steps"></a>Próximas etapas
Agora que você tem a versão mais recente de saudação do SSDT, você está pronto muito[conectar] [ connect] tooyour SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Baixar o Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
