---
title: "Migrar: Utilitário de Migração do Data Warehouse | Microsoft Docs"
description: Migre tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Utilitário de Migração do Data Warehouse (visualização)
> [!div class="op_single_selector"]
> * [Baixar o Utilitário de Migração][Download Migration Utility]
> 
> 

Olá utilitário de migração do Data Warehouse é que uma ferramenta projetada toomigrate esquema e dados do SQL Server e banco de dados do SQL Azure tooAzure SQL Data Warehouse. Durante a migração de esquema, a ferramenta Olá mapeia automaticamente esquema correspondente de saudação do toodestination de origem. Depois de migrar o esquema hello, ferramentas de saudação fornece Olá opção toomove dados com scripts gerados automaticamente.

Além disso, tooschema e migração de dados, essa ferramenta permite Olá opção toogenerate compatibilidade relatórios resumem incompatibilidades entre instâncias de origem e destino Olá que o impediriam simplificada migração.

## <a name="get-started"></a>Introdução
Como um pré-requisito para a instalação, você precisará de scripts de migração toorun do utilitário de linha de comando de BCP hello e relatório de compatibilidade do Office tooview hello. Depois de iniciar o hello executável que é baixado você será tooaccept solicitada EULA padrão antes de ferramenta Olá será instalada.

Além disso, Olá toorun Utiliy de migração, você será necessário Olá um no banco de dados de saudação que você está procurando toomigrate as seguintes permissões: CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION.

### <a name="launching-hello-tool-and-connecting"></a>Ferramenta de saudação e conectar-se
Ferramenta de inicialização de saudação clicando no ícone de área de trabalho de saudação que aparece após instalar. Ao abrir a ferramenta Olá, você será solicitado com uma página de conexão inicial, onde você pode escolher a origem e destino para a ferramenta de migração hello. No momento, há suporte para o SQL Server e o Banco de Dados SQL do Azure como origens e para o SQL Data Warehouse como um destino. Depois de selecionar essa opção você será solicitado o servidor de origem tooyour tooconnect preenchendo em nome do servidor e autenticação e, em seguida, clicando em 'Conectar'.

Depois de autenticar, a ferramenta de saudação mostrará uma lista de bancos de dados que estão presentes no servidor de saudação que você está conectado. Você pode começar a migração de saudação selecionando um banco de dados que você gostaria de toomigrate e, em seguida, clicando em 'Migrar selecionada'.

## <a name="migration-report"></a>Relatório de migração
Selecionar 'Verificar a compatibilidade do banco de dados' na ferramenta de saudação irá gerar um relatório de resumo de todas as incompatibilidades de objeto no banco de dados de saudação solicitado toomigrate. Uma lista mais ampla de algumas das Olá funcionalidade do SQL Server que não está presente no SQL Data Warehouse pode ser encontrada em nosso [documentação de migração][migration documentation]. Depois Olá relatório é gerado, você será capaz de toosave e relatório Olá abrir no Excel.

Observe que, quando a geração de esquema de migração hello, a maioria dos problemas identificados como 'Object' será ajustada em migração imediata do pedido tooallow desses dados. Analise Olá alterações tooensure você não quiser ajustes adicionais toomake antes de aplicar o esquema de saudação.

## <a name="migrate-schema"></a>Migrar o esquema
Após a conexão, selecionando 'Migrar o esquema' irá gerar um script de migração de esquema para tabelas de saudação selecionada. Essa estrutura de saudação do script portas da tabela Olá, mapeia dados incompatíveis tipos toomore compatível formulários e cria o esquema e as credenciais de segurança se isso é indicado pelo usuário Olá nas configurações de migração de saudação. Esse código pode ser executado na instância do SQL Data Warehouse de Olá direcionado, tooa arquivo salvo, copiado na área de transferência tooyour ou mesmo editado na linha antes de fazer mais nada.  

Como mencionado acima, quando migrar migração do esquema revisão Olá alterações que Olá ferramenta fez em ordem tooensure que que você compreenda plenamente-los.  

## <a name="migrate-data"></a>Migrar dados
Clicando em opção de migrar dados Olá, é possível gerar scripts BCP que moverá os arquivos de tooflat dados primeiro em seu servidor e, em seguida, diretamente no Data Warehouse do SQL. É recomendável que esse processo para transferir pequenas quantidades de dados e, como repetições não são internos e falhas podem ocorrer se houver uma perda de conexão de rede de saudação. Em ordem toorun isso, você precisará toohave Olá de linha de comando utilitário BCP instalado e esquema Olá para dados saudação já deve ter sido criada.

Depois de preencher os parâmetros de saudação anteriormente, você simplesmente precisa tooclick executar migração e será gerado um conjunto de dois pacotes tooyour especificado local. Execute o arquivo de exportação de saudação dados de pedidos tooexport da fonte de migração em arquivos simples e execute o arquivo de importação Olá em ordem tooimport seus dados no SQL Data Warehouse.

## <a name="next-steps"></a>Próximas etapas
Agora que você já migrou alguns dados, confira como muito[desenvolver][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
