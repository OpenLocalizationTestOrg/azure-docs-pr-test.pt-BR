---
title: "aaaOverview de banco de dados do Azure para o serviço de banco de dados relacional do MySQL | Microsoft Docs"
description: "Visão geral do hello banco de dados do Azure para o serviço de banco de dados relacional do MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>O que é o Banco de Dados do Azure para MySQL? Introdução ao serviço
Banco de dados do Azure para MySQL é um serviço de banco de dados relacional no hello com base em nuvem da Microsoft [MySQL Community Edition](https://www.mysql.com/products/community/) mecanismo de banco de dados.  O Banco de Dados do Azure para MySQL fornece:

- Desempenho previsível em vários níveis de serviço
- Escalabilidade dinâmica sem tempo de inatividade do aplicativo
- Alta disponibilidade interna
- Proteção de dados

Esses recursos não precisam de quase nenhuma administração e todos são fornecidos sem nenhum custo adicional. Elas permitem que você toofocus desenvolvimento rápido de aplicativos e acelerando o toomarket de tempo, em vez de alocação de tempo e recursos toomanaging VMs e infraestrutura. Além disso, você pode continuar toodevelop seu aplicativo com hello abrir ferramentas de software e plataforma de sua escolha e entregar com velocidade de saudação e a eficiência de sua empresa exige sem ter que toolearn novas habilidades.

![Diagrama conceitual do Banco de Dados do Azure para MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Este artigo é um banco de dados de tooAzure de Introdução para MySQL principais conceitos e tooperformance de recursos relacionados, escalabilidade e capacidade de gerenciamento, com detalhes de tooexplore links. Consulte que esses rápida inicia tooget que é iniciado:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um servidor de Banco de Dados do Azure para MySQL usando a CLI do Azure](quickstart-create-mysql-server-database-using-azure-cli.md)

Para ver diversos exemplos da CLI do Azure, consulte:
- [Exemplos da CLI do Azure para o Banco de Dados do Azure para MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste de desempenho e dimensionamento sem tempo de inatividade
O serviço de Banco de Dados do Azure para MySQL oferece duas camadas de serviço: Básico e Standard. Cada camada oferece desempenho diferente e cargas de trabalho de banco de dados do recursos toosupport tooheavyweight leve. Você pode criar seu primeiro aplicativo em um banco de dados pequeno por alguns dólares, um mês, em seguida, alterar seu tooscale de nível de serviço com necessidades de sua solução sem tempo de inatividade. Dimensionamento dinâmico permite que o banco de dados tootransparently responder toorapidly que alterações de requisitos de recursos. Você paga apenas pelos recursos de saudação que é necessário, quando necessário.

## <a name="monitoring-and-alerting"></a>Monitoramento e alertas
Como você sabe Olá parar clique com botão direito ao discar para cima e para baixo? Usar monitoramento de desempenho internas hello e recursos, combinados com as classificações de desempenho de Olá com base na unidade de computação de alerta. Usando esses recursos, você pode avaliar rapidamente impacto de saudação de dimensionamento para cima ou para baixo com base no seu atual ou necessidades de desempenho do projeto. Consulte [Conceitos: camadas de serviço](concepts-service-tiers.md) para obter detalhes.

## <a name="keep-your-app-and-business-running"></a>Mantenha seus aplicativos e a continuidade dos negócios
O SLA (Contrato de Nível de Serviço) de disponibilidade de 99,99% do Azure, que é líder do setor e é alimentado por uma rede global de datacenters gerenciados pela Microsoft, ajuda a manter seu aplicativo em execução de forma ininterrupta. Cada banco de dados do Azure para o MySQL server, você tirar proveito de segurança internas, a tolerância a falhas e proteção de dados que você teria toobuy ou design, criar e gerenciar. Com o banco de dados do Azure para MySQL, você pode usar a restauração point-in-time toorecover tooan um servidor de estado anterior, a partir de 35 dias.

## <a name="secure-your-data"></a>Proteja seus dados
Os serviços de banco de dados do Azure têm uma tradição de segurança de dados que o Banco de Dados do Azure para MySQL mantém, com recursos que limitam o acesso, protegem dados em repouso e em movimento e ajudam a monitorar atividades. Visite Olá [Azure Trust Center](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) para obter informações sobre a segurança da plataforma do Azure.

saudação de banco de dados do Azure para o serviço do MySQL usa criptografia de armazenamento para dados em repouso. Incluindo backups, de dados são criptografados em disco (com exceção de saudação do arquivos temporários criados pelo mecanismo de saudação durante a execução de consultas). serviço Olá usa criptografia AES de 256 bits que é incluída na criptografia de armazenamento do Azure e chaves de saudação são gerenciado do sistema. A criptografia de armazenamento está sempre ativada e não pode ser desabilitada.

Por padrão, Olá banco de dados do Azure para o serviço MySQL é configurado toorequire [segurança de conexão SSL](./concepts-ssl-connection-security.md) para dados em movimento em rede hello. Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.  Opcionalmente, você pode desabilitar exigir SSL para conectar-se o serviço de banco de dados tooyour se seu aplicativo cliente não oferece suporte a conectividade SSL.

## <a name="next-steps"></a>Próximas etapas
Agora que você ler um tooAzure Introdução banco de dados MySQL e respondeu a pergunta hello "Como está o banco de dados do Azure para MySQL?", você está pronto para:
- Consulte a página para comparações de custo e calculadoras de preços de saudação. [Preços](https://azure.microsoft.com/pricing/details/mysql/)
- Comece com a criação do seu primeiro servidor. [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Crie seu primeiro aplicativo em Python, Ruby, PHP C\#, Java, Node. js: [bibliotecas de conectividade usados tooconnect tooAzure banco de dados para MySQL](concepts-connection-libraries.md)
