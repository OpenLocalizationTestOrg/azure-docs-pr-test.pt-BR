---
title: "segurança aaaDatabase - banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como o Azure Cosmos DB fornece proteção de banco de dados e segurança para seus dados."
keywords: "segurança do banco de dados nosql, segurança de informações, segurança de dados, criptografia de banco de dados, proteção de banco de dados, políticas de segurança, teste de segurança"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Segurança de banco de dados do Azure Cosmos DB

Este artigo aborda práticas recomendadas de segurança de banco de dados e os principais recursos oferecidos pelo banco de dados do Azure Cosmos toohelp impedir, detectar e responder toodatabase violações.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Novidades na segurança do Azure Cosmos DB?

A criptografia em repouso agora está disponível para documentos e backups armazenados no Azure Cosmos DB em todas as regiões do Azure. A criptografia em repouso é aplicada automaticamente para clientes novos e existentes nessas regiões. Não há nenhuma necessidade tooconfigure nada; e você obtém Olá mesmo latência grande, a taxa de transferência, a disponibilidade e a funcionalidade como antes de benefícios Olá saber seus dados são seguras e protegidas com criptografia em repouso.

## <a name="how-do-i-secure-my-database"></a>Como fazer para proteger meu banco de dados? 

Segurança de dados é uma responsabilidade compartilhada entre você, Olá cliente e o provedor de banco de dados. Dependendo do provedor de banco de dados de saudação que você escolher, Olá responsabilidade que executar pode variar. Se você escolher uma solução local, será necessário tooprovide tudo da segurança de toophysical de proteção de ponto de extremidade do seu hardware - que não é tarefa fácil. Se você escolher um provedor de banco de dados em nuvem PaaS, como o Azure Cosmos DB, sua área de interesse será consideravelmente reduzida. Olá após a imagem, emprestada da Microsoft [responsabilidades compartilhado para a computação em nuvem](https://aka.ms/sharedresponsibility) white paper, mostra como sua responsabilidade diminui com um provedor de PaaS, como o banco de dados do Azure Cosmos.

![Responsabilidades do cliente e do provedor de banco de dados](./media/database-security/nosql-database-security-responsibilities.png)

Olá anterior componentes do diagrama mostra nuvem de alto nível de segurança, mas os itens que você precisa tooworry sobre especificamente para sua solução de banco de dados? E como você pode comparar soluções tooeach outros? 

É recomendável Olá seguindo a lista de verificação de requisitos de quais sistemas de banco de dados toocompare:

- Configurações de firewall e de segurança de rede
- Autenticação de usuário e controles de usuário refinados
- Dados de tooreplicate capacidade globalmente para falhas regionais
- Capacidade tooperform failovers de um data center tooanother
- Replicação de dados locais em um data center
- Backup de dados automático
- Restauração de dados excluídos de backups
- Proteger e isolar dados confidenciais
- Monitoramento de ataques
- Responder tooattacks
- Restrições de controle do capacidade limite toogeo dados tooadhere toodata
- Proteção física dos servidores em data centers protegidos

E embora possa parecer óbvio, recente [violações de banco de dados em grande escala](http://thehackernews.com/2017/01/mongodb-database-security.html) lembrá-nos sobre a importância simples, mas crítico Olá Olá requisitos a seguir:
- Corrigida servidores que são atualizados toodate
- Criptografia HTTPS por padrão/SSL
- Contas administrativas com senhas fortes

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Como o Azure Cosmos DB protege meu banco de dados?

Vamos examinar novamente Olá anterior lista - quantos esses requisitos de segurança de banco de dados do Azure Cosmos oferece? Todos.

Vamos examinar cada um deles em detalhes.

|Requisito de segurança|Abordagem de segurança do Azure Cosmos DB|
|---|---|---|
|Segurança de rede|Usando um firewall IP é Olá primeira camada de proteção toosecure seu banco de dados. O Azure Cosmos DB dá suporte a controles de acesso baseado em IP controlados por política para suporte de firewall de entrada. controles de acesso com base em IP Hello são semelhantes toohello as regras de firewall usadas pelos sistemas de banco de dados tradicional, mas eles são expandidos para que uma conta de banco de dados do banco de dados do Azure Cosmos só é acessível de um conjunto aprovado das máquinas ou serviços de nuvem. <br><br>Banco de dados do Azure Cosmos permite que você tooenable um endereço IP específico (168.61.48.0), um intervalo IP (168.61.48.0/8) e combinações de IPs e intervalos. <br><br>Todas as solicitações provenientes de computadores fora dessa lista de permissões são bloqueadas pelo Azure Cosmos DB. Solicitações de aprovação máquinas e serviços de nuvem, em seguida, deverá concluir Olá toobe de processo de autenticação fornecido recursos de toohello de controle de acesso.<br><br>Saiba mais em [Suporte ao firewall do Azure Cosmos DB](firewall-support.md).|
|Autorização|O Azure Cosmos DB usa o HMAC (código de autenticação de mensagem baseado em hash) para autorização. <br><br>Cada solicitação é transformado em hash usando a chave de conta secreta de saudação e subsequentes hash de codificado em base 64 Olá é enviado com cada chamada tooAzure Cosmos DB. Olá toovalidate solicitar hello Azure Cosmos DB serviço usa Olá chave secreta correta e propriedades toogenerate um hash, em seguida, ele compara o valor de saudação com hello na solicitação de saudação. Se dois valores de saudação coincidirem, operação hello está autorizada com êxito e Olá solicitação é processada, caso contrário, haverá uma falha de autorização e Olá solicitação será rejeitada.<br><br>Você pode usar um [chave mestra](secure-access-to-data.md#master-keys), ou um [token de recurso](secure-access-to-data.md#resource-tokens) permitindo que o recurso de tooa de acesso refinado como um documento.<br><br>Saiba mais em [tooAzure Cosmos DB recursos de proteção de acesso](secure-access-to-data.md).|
|Usuários e permissões|Usando Olá [chave mestra](#master-key) conta hello, você pode criar recursos de usuário e recursos de permissão por banco de dados. Um [token de recurso](#resource-token) está associada uma permissão em um banco de dados e determina se o usuário Olá tem acesso (leitura / gravação, somente leitura, ou nenhum acesso) tooan o recurso de aplicativo no banco de dados de saudação. Os recursos do aplicativo incluem coleções, documentos, anexos, procedimentos armazenados, gatilhos e UDFs. o token de recurso Olá é, em seguida, usado durante a autenticação tooprovide ou nega acesso toohello recursos.<br><br>Saiba mais em [tooAzure Cosmos DB recursos de proteção de acesso](secure-access-to-data.md).|
|Integração do Active Directory (RBAC)| Você também pode fornecer a conta de banco de dados do access toohello usando o controle de acesso (IAM) em Olá portal do Azure, conforme mostrado na captura de tela de saudação após esta tabela. O IAM fornece controle de acesso baseado em função e integra-se ao Active Directory. Você pode usar funções internas ou personalizadas para indivíduos e grupos, conforme mostrado no Olá a imagem a seguir.|
|Replicação global|Banco de dados do Azure Cosmos oferece completa distribuição global, o que permite que você tooreplicate sua tooany de dados de data centers de todo o mundo do Azure com hello clique de um botão. Replicação global permite dimensionamento global e fornecer acesso de baixa latência tooyour dados em torno de Olá, mundo.<br><br>No contexto de saudação de segurança, replicação global assegura a proteção de dados contra falhas regionais.<br><br>Saiba mais em [Distribuir dados globalmente](distribute-data-globally.md).|
|Failovers regionais|Se você tiver replicado seus dados em mais de um data center, o Azure Cosmos DB reverterá automaticamente aas operações, caso um data center regional fique offline. Você pode criar uma lista priorizada de regiões de failover usando Olá regiões em que os dados são replicados. <br><br>Saiba mais em [Failovers regionais no Azure Cosmos DB](regional-failover.md).|
|Replicação local|Mesmo em um único data center, o banco de dados do Azure Cosmos replica automaticamente os dados para alta disponibilidade fornecendo Olá escolha de [níveis de consistência](consistency-levels.md). Isso garante um  [SLA de disponibilidade de tempo de atividade de 99,99%](https://azure.microsoft.com/support/legal/sla/cosmos-db) e é fornecido com uma garantia financeira: algo que nenhum outro serviço de banco de dados pode oferecer.|
|Backups online automatizados|Os bancos de dados do Azure Cosmos DB passam por backup e são armazenados regularmente em um repositório com redundância geográfica. <br><br>Saiba mais em [Backup e restauração online automáticos com o Azure Cosmos DB](online-backup-and-restore.md).|
|Restaurar dados excluídos|Hello automatizados backups online podem ser usadas toorecover dados você pode ter excluído acidentalmente backup muito ~ 30 dias após o evento de saudação. <br><br>Saiba mais em [Backup e restauração online automáticos com o Azure Cosmos DB](online-backup-and-restore.md)|
|Proteger e isolar dados confidenciais|Todos os dados em regiões Olá listados na [novidades?](#whats-new) agora são criptografados em repouso.<br><br>PII e outros dados confidenciais podem ser isolado toospecific coleções e leitura / gravação ou acesso somente leitura pode ser limitado toospecific usuários.|
|Monitorar ataques|Com o registro em log de auditoria e os logs de atividade, você pode monitorar as atividades normais e anormais de sua conta. Você pode exibir as operações que foram executadas em seus recursos, que iniciou a operação de saudação quando ocorreu a operação hello, status de saudação da operação de saudação e muito mais, conforme mostrado na captura de tela de saudação após esta tabela.|
|Responder tooattacks|Depois que você entraram em contato com o suporte do Azure tooreport um ataque em potencial, um processo de resposta a incidentes etapa 5 é iniciado. meta de saudação do processo da etapa 5 de Olá é toorestore segurança de serviço normal e operações mais rápido possível depois que um problema foi detectado e uma investigação é iniciada.<br><br>Saiba mais em [resposta de segurança do Microsoft Azure na nuvem de saudação](https://aka.ms/securityresponsepaper).|
|Isolamento geográfico|O Azure Cosmos DB garante a governança de dados e conformidade em regiões soberanas (por exemplo, Alemanha, China, US Gov).|
|Instalações protegidas|Os dados do Azure Cosmos DB são armazenados em SSDs, nos data centers protegidos do Azure.<br><br>Saiba mais em [Datacenters globais da Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|Criptografia HTTPS/SSL/TLS|Todas as interações do cliente com o serviço do Azure Cosmos DB são impostas por SSL/TLS 1.2. Além disso, toda replicação dentro do datacenter e entre datacenters é imposta por SSL/TLS 1.2.|
|Criptografia em repouso|Todos os dados armazenados no Azure Cosmos DB são criptografados em repouso. Saiba mais em [Criptografia em repouso do Azure Cosmos DB](.\database-encryption-at-rest.md)|
|Servidores com patches|Como um banco de dados gerenciado, Azure Cosmos DB elimina Olá necessidade toomanage e patch servidores, que foi feito para você automaticamente.|
|Contas administrativas com senhas fortes|Seu disco rígido toobelieve que pelo menos necessário toomention esse requisito, mas ao contrário de alguns dos nossos concorrentes, é impossível toohave uma conta de administrador sem senha no banco de dados do Azure Cosmos.<br><br> A segurança via autenticação baseada em segredo de SSL e HMAC está incorporada por padrão.|
|Certificações de proteção de dados e de segurança|O Azure Cosmos DB tem as certificações [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [EUMC (European Model Clauses)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) e [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA). Outras certificações estão em andamento.|

Hello seguinte captura de tela mostra a integração do Active directory (RBAC) usando o controle de acesso (IAM) no portal do Azure de saudação: ![(IAM) do controle de acesso no hello portal do Azure - demonstrando a segurança de banco de dados](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Olá seguinte captura de tela mostra como você pode usar o log de auditoria e logs de atividades toomonitor sua conta: ![dos logs de atividades para o banco de dados do Azure Cosmos](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes sobre chaves mestras e tokens de recurso, consulte [tooAzure de acesso protegendo dados do banco de dados do Cosmos](secure-access-to-data.md).

Para obter mais detalhes sobre as certificações da Microsoft, confira [Central de Confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/).
