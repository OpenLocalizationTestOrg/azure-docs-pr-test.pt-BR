---
title: "aaaTechnical pré-requisitos para a criação de um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Entender os requisitos para a criação de um serviço de dados toodeploy hello e vender em hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Técnicas pré-requisitos para a criação de um serviço de dados oferecem para hello Azure Marketplace
> [!IMPORTANT]
> **Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.** Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners). Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Processo Olá completamente antes de começar de ler e entender por cada etapa é executada. Tanto quanto possível, você deve preparar as informações da sua empresa e outros dados, baixe as ferramentas necessárias e/ou criar componentes técnicos antes de começar o processo de criação de oferta de saudação.

Você deve ter Olá prontos antes de começar o processo de saudação de itens a seguir:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Tomar uma decisão sobre qual tecnologia será usada toopublish sua oferta de serviço de dados
Um Editor pode decidir entre várias tecnologias ao publicar o Serviço de Dados no Azure Marketplace. Olá principais tecnologias com suporte descritas abaixo. Independentemente qual tecnologia é usada toopublish Olá serviço de dados, usuário final de saudação consome dados de saudação por meio de saudação **feed OData** expostos pelo serviço do Azure Marketplace. Encontre informações completas sobre o serviço do OData em [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>Banco de Dados SQL do Azure
Ter o conjunto de dados pronto no SQL Azure é responsabilidade do Editor. Você precisará toosubscribe tooAzure, provisionar tamanho apropriado de banco de dados e carregar os dados no banco de dados do SQL Azure. O Publisher também é responsável tookeep seus dados sempre atualizados. Para obter mais informações sobre como assinar tooAzure serviços que você pode encontrar no [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Ao mover dados Olá para o SQL Azure, hello Azure Marketplace pode expor tabelas e exibições. Olá Publisher pode especificar quais tabelas/modos de exibição e as colunas são toohello exposto ao usuário final. Provedor de conteúdo adicional Olá também pode especificar quais colunas podem ser consultadas por usuários finais de saudação e quais são retornados apenas na carga de saudação. Isso fornece um alto nível de flexibilidade sobre quais dados no banco de dados de saudação devem ser expostos. Colunas que podem ser consultadas necessário toobe sustentado por um ou mais índices de banco de dados.

## <a name="rest-based-web-service"></a>Serviço Web baseado em REST
Protocolo com suporte: **somente HTTPS**

Serviços com base REST existentes podem ser expostos por meio de saudação do Azure Marketplace. Como saudação de conjunto de dados é sempre toohello exposto ao usuário final como um feed OData, Olá serviço do Azure Marketplace precisa toomap capaz de toobe Olá serviço tooa serviço OData com base. toodo para Olá REST com base em pontos de extremidade necessário tooexpose todos os parâmetros como parâmetros HTTP.

carga Olá precisa toobe em um formulário que pode ser mapeado para uma resposta ATOM. Portanto, a resposta de saudação dos serviços de saudação precisa toobe em formato XML e só pode conter um elemento de repetição que contém valores de carga hello (como o conjunto de registros). Olá serviço do Azure Marketplace mapeará Olá repetindo o nó de entrada de toohello em valores de carga ATOM e hello em nós de propriedade do nó de entrada hello.

Informações de autorização (como a API chave, autenticação token, etc.) devem toobe fornecida como um parâmetro HTTP ou no cabeçalho HTTP de saudação (par chave-valor) – também há suporte para autenticação básica. Precisa de uma chave válida toobe fornecido e todas as solicitações através do Azure Marketplace estão sendo feitas por meio de chave. Usuário de monitoramento e a cobrança ocorre na camada do hello Azure Marketplace.

Erros retornados pelo serviço Olá necessário toobe mapeado em códigos de status HTTP. No caso de serviço Olá retorna um XML que contém o erro Olá esses serão toobe mapeado por códigos de status de tooHTTP de serviço do hello Azure Marketplace.

## <a name="soap-based-web-services"></a>Serviços Web baseados em SOAP
Protocolo: **somente HTTPS**

requisitos de saudação são Olá mesmo como na seção de serviço com base REST hello. Olá única diferença é que os parâmetros também podem ser fornecidos em um corpo XML que está sendo lançado serviço toohello do publicador com cada solicitação feita através do Azure Marketplace. Isso significa que o usuário de saudação de parâmetros HTTP fornece no hello front-end está sendo convertido em elementos XML de um documento XML que está sendo lançado com o serviço web de saudação solicitação toohello do provedor de conteúdo.

## <a name="odata-based-web-services"></a>Serviços Web baseados em OData
Protocolo: **somente HTTPS**

Dados podem ser expostos como um serviço de OData tooAzure Marketplace. Olá sistema vai toopass serviço Olá por meio e substitui a raiz de saudação do serviço de saudação com raiz de serviço do Azure Marketplace hello – tooensure todas as chamadas subsequentes percorrer Azure Marketplace.

Serviços OData não basta toogo em relação a um banco de dados back-end de saudação. OData oferece suporte a qualquer tipo de serviço de saudação do armazenamento ou business lógica toodrive.

## <a name="next-steps"></a>Próximas etapas
Agora que você revisar os pré-requisitos de saudação e concluir tarefas necessárias hello, você pode continuar com hello criando sua oferta de serviço de dados como Olá detalhada em [guia de publicação de serviço de dados](marketplace-publishing-data-service-creation.md).

Ou, se você quiser tooreview Olá processo geral e artigos respectivos Olá para cada uma das fases de publicação de saudação, visite o artigo Olá [guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
