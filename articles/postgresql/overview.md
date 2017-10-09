---
title: "aaaOverview de banco de dados do Azure para o serviço de banco de dados relacional PostgreSQL | Microsoft Docs"
description: "Fornece uma visão geral do serviço de banco de dados relacional Banco de Dados do Azure para PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>O que é o Banco de Dados do Azure para PostgreSQL?

Banco de dados do Azure para PostgreSQL é um serviço de banco de dados relacional no hello nuvem da Microsoft desenvolvido para desenvolvedores com base na versão da comunidade de saudação do código-fonte aberto [PostgreSQL](https://www.postgresql.org/) mecanismo de banco de dados. Esse serviço está na fase de visualização pública. O Banco de Dados do Azure para PostgreSQL fornece:
- Desempenho previsível em vários níveis de serviço
- Escalabilidade dinâmica sem tempo de inatividade do aplicativo
- Alta disponibilidade interna
- Proteção de dados

Todos esses recursos não precisam de quase nenhuma administração e todos são fornecidos sem nenhum custo adicional. Esses recursos permitem que você toofocus desenvolvimento rápido de aplicativos e acelerando o toomarket de tempo, em vez de alocação de tempo e recursos toomanaging VMs e infraestrutura. Além disso, você pode continuar toodevelop seu aplicativo com hello abrir ferramentas de software e plataforma de sua escolha e entregar com velocidade de saudação e a eficiência de sua empresa exige sem ter que toolearn novas habilidades. 

Este artigo é uma introdução tooAzure banco de dados PostgreSQL principais conceitos e tooperformance de recursos relacionados, escalabilidade e gerenciamento. Consulte que esses rápida inicia tooget que é iniciado:

- [Criar um servidor de Banco de Dados do Azure para PostgreSQL usando o portal do Azure](quickstart-create-server-database-portal.md)
- [Criar um banco de dados do Azure para PostgreSQL usando Olá CLI do Azure](quickstart-create-server-database-azure-cli.md)

Para ver vários exemplos da CLI do Azure e do PowerShell, consulte:

- [Exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste de desempenho e dimensionamento sem tempo de inatividade

O serviço de Banco de Dados do Azure para PostgreSQL atualmente oferece duas camadas de serviço: Básico e Standard. Cada camada de serviço oferece [diferentes níveis de desempenho, recursos e garantias IOPS](concepts-service-tiers.md) cargas de trabalho de banco de dados do toosupport tooheavyweight leve. Você pode criar seu primeiro aplicativo em um servidor de pequeno para alguns dinheiro um mês e, em seguida, [alterar o nível de desempenho Olá](scripts/sample-scale-server-up-or-down.md) no serviço de camada manualmente ou programaticamente qualquer necessidades de saudação do tempo toomeet de sua solução. Você pode fazer isso sem o aplicativo do tempo de inatividade tooyour ou tooyour clientes. Habilita o dimensionamento dinâmico tootransparently seu banco de dados responder toorapidly alterando os requisitos de recursos e permite que você tooonly pagar por recursos de saudação que é necessário quando você precisar deles.

## <a name="monitoring-and-alerting"></a>Monitoramento e alertas
Como decidir quando toodial para cima e para baixo? Use o monitoramento de desempenho internas hello e recursos, combinados com as classificações de desempenho de Olá com base em unidades de computação de alerta. Usando essas ferramentas, você pode avaliar rapidamente o impacto de saudação do aumento de escala de computação unidades ou inativo com base em suas necessidades de desempenho atual ou projetado. Para obter detalhes, consulte [Opções e desempenho do Banco de Dados do Azure para PostgreSQL: compreender o que está disponível em cada camada de serviço](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Mantenha seus aplicativos e a continuidade dos negócios
O SLA (Contrato de Nível de Serviço) de disponibilidade de 99,99% do Azure (indisponível na versão prévia), que é líder do setor e é alimentado por uma rede global de datacenters gerenciados pela Microsoft, ajuda a manter seu aplicativo em execução de forma ininterrupta. Cada banco de dados do Azure para servidor PostgreSQL, você tirar proveito de segurança internas, a tolerância a falhas e proteção de dados que você teria toobuy ou design, criar e gerenciar. Com o banco de dados do Azure para PostgreSQL, cada camada de serviço oferece um conjunto abrangente de recursos de continuidade de negócios e opções que você pode usar tooget para cima e em execução e fique dessa maneira. Você pode usar [restauração point-in-time](howto-restore-server-portal.md) tooreturn tooan um banco de dados de estado anterior, a partir de 35 dias. Além disso, se o datacenter Olá hospeda seus bancos de dados passa por uma interrupção, você pode restaurar bancos de dados de redundância geográfica cópias de backups recentes.

## <a name="secure-your-data"></a>Proteja seus dados
Os serviços de banco de dados do Azure têm uma tradição de segurança de dados que o Banco de Dados do Azure para PostgreSQL mantém, com recursos que limitam o acesso, protegem dados em repouso e em movimento e ajudam a monitorar atividades. Visite Olá [Azure Trust Center](https://www.microsoft.com/TrustCenter/Security/default.aspx) para obter informações sobre a segurança da plataforma do Azure.

saudação de banco de dados PostgreSQL serviço usa criptografia de armazenamento para dados em repouso. Incluindo backups de dados são criptografados em disco (com exceção de saudação do arquivos temporários criados pelo mecanismo de saudação durante a execução de consultas). serviço Olá usa criptografia AES de 256 bits que é incluída na criptografia de armazenamento do Azure e chaves de saudação são gerenciado do sistema. A criptografia de armazenamento está sempre ativada e não pode ser desabilitada.

Por padrão, Olá banco de dados PostgreSQL serviço é configurado toorequire [segurança de conexão SSL](./concepts-ssl-connection-security.md) para dados em movimento em rede hello. Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.  Opcionalmente, você pode desabilitar exigir SSL para conectar-se o serviço de banco de dados tooyour se seu aplicativo cliente não oferece suporte a conectividade SSL.

## <a name="next-steps"></a>Próximas etapas
- Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/postgresql/) para comparações de custo e calculadoras.
- Comece pela [criação do seu primeiro Banco de Dados do Azure para PostgreSQL](./quickstart-create-server-database-portal.md).
- Crie seu primeiro aplicativo no Python, PHP, Ruby, C\#, Java, Node.js: [Bibliotecas de conexão](./concepts-connection-libraries.md)
