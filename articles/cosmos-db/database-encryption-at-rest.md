---
title: 'Criptografia de banco de dados em repouso: Azure Cosmos DB | Microsoft Docs'
description: "Saiba como o Azure Cosmos DB fornece criptografia padrão de todos os dados."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Criptografia de banco de dados em repouso do Azure Cosmos DB

Criptografia em repouso é uma frase que normalmente se refere toohello criptografia de dados em dispositivos de armazenamento não volátil como unidades de estado sólido (SSDs) e unidades de disco rígido (HDDs). O Cosmos DB armazena seus bancos de dados principais em SSDs. Seus anexos de mídia e backups são armazenados no armazenamento de Blobs do Azure, do qual geralmente é feito backup por HDDs. Com versão de saudação de criptografia em repouso para Cosmos banco de dados, todos os seus bancos de dados, anexos de mídia e backups são criptografados. Seus dados são criptografados em trânsito agora (pela rede Olá) e em repouso (armazenamento não volátil), fornecendo criptografia de ponta a ponta.

Como um serviço de PaaS, Cosmos banco de dados é muito fácil toouse. Como todos os dados de usuário armazenados no banco de dados do Cosmos é criptografado em repouso e em transporte, você não tem tootake qualquer ação. Outro tooput de forma que isso é que a criptografia em rest está ativada, por padrão. Não há nenhum tooturn controles-lo ou desativar. Podemos fornecer esse recurso enquanto continuarmos toomeet nosso [SLAs de desempenho e disponibilidade](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Implementar a criptografia em repouso

A criptografia em repouso é implementada usando várias tecnologias de segurança, incluindo sistemas seguros de armazenamento de chaves, redes criptografadas e APIs criptográficas. Sistemas que descriptografarem e processam dados têm toocommunicate com sistemas de gerenciamento de chaves. diagrama de saudação mostra como o armazenamento do gerenciamento de dados e hello criptografado de chaves é separado. 

![Diagrama de design](./media/database-encryption-at-rest/design-diagram.png)

fluxo básico a saudação de uma solicitação de usuário é o seguinte:
- conta de banco de dados de usuário Olá fica pronta e chaves de armazenamento são recuperadas por meio de um provedor de recursos do serviço de gerenciamento de toohello de solicitação.
- Um usuário cria uma conexão tooCosmos banco de dados por meio do transporte HTTPS/seguro. (detalhes de saudação abstrato do hello SDKs).
- usuário Olá envia um toobe do documento JSON armazenado Olá criado anteriormente a conexão segura.
- documento JSON Olá é indexado, a menos que o usuário Olá desativou a indexação.
- Olá documento JSON e dados do índice são gravados toosecure armazenamento.
- Periodicamente, dados lidos do armazenamento seguro de saudação e backup toohello armazenamento de Blob do Azure criptografado.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>P: Qual é o custo adicional do armazenamento do Azure se a Criptografia do Serviço de Armazenamento é habilitada?
R: Não há qualquer custo adicional.

### <a name="q-who-manages-hello-encryption-keys"></a>P: que gerencia chaves de criptografia Olá?
R: Olá chaves são gerenciadas pela Microsoft.

### <a name="q-how-often-are-encryption-keys-rotated"></a>P: Com que frequência as chaves de criptografia são trocadas?
R: A Microsoft tem um conjunto de diretrizes internas para rotação de chave de criptografia, que o Cosmos DB segue. as diretrizes específicas da saudação não são publicadas. A Microsoft publica Olá [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), que é visto como um subconjunto de diretrizes interno e tem práticas recomendadas útil para desenvolvedores.

### <a name="q-can-i-use-my-own-encryption-keys"></a>P: Posso usar minhas próprias chaves de criptografia?
R: cosmos banco de dados é um serviço de PaaS e trabalhamos tookeep rígido Olá serviço fácil toouse. Observamos que essa pergunta geralmente é feita como uma pergunta substituta para o cumprimento de um requisito de conformidade, como as normas PCI-DSS. Como parte da construção esse recurso, trabalhamos com conformidade auditores tooensure que os clientes que usam o banco de dados do Cosmos atenderem seus requisitos sem Olá necessidade toomanage as próprias chaves.
Como resultado, no momento não oferecemos usuários Olá opção tooburden-se com o gerenciamento de chaves.

### <a name="q-what-regions-have-encryption-turned-on"></a>P: Em quais regiões a criptografia está ativada?
R: A criptografia está ativada para todos os dados do usuário em todas as regiões do Azure Cosmos DB.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>P: criptografia afeta a latência de desempenho hello e taxa de transferência SLAs?
R: não há nenhum impacto ou alterações toohello SLAs de desempenho agora que a criptografia em repouso está habilitada para todas as contas novas e existentes. Você pode ler mais sobre Olá [SLA para o banco de dados do Cosmos](https://azure.microsoft.com/support/legal/sla/cosmos-db) página garantias mais recentes do toosee hello.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>P: o emulador local Olá oferecer suporte à criptografia em repouso?
R: emulador de Olá é uma ferramenta de desenvolvimento/teste autônoma e não usa os serviços de gerenciamento de chaves Olá Olá gerenciado Cosmos DB serviço usa. Nossa recomendação é tooenable BitLocker nas unidades em que você está armazenando dados de teste do emulador confidenciais. Olá [emulador suporta alterar diretório de dados padrão de saudação](local-emulator.md) , bem como o uso de um local conhecido.

## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral de segurança de banco de dados do Cosmos e melhorias mais recentes hello, consulte [segurança de banco de dados do banco de dados do Azure Cosmos](database-security.md).
Para obter mais informações sobre certificações da Microsoft, consulte Olá [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).
