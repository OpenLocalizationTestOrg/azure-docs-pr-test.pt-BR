---
title: "Visão geral de segurança de banco de dados aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos recursos de segurança de banco de dados do Azure hello."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Visão geral de segurança do banco de dados do Azure

A segurança é uma das principais preocupações durante o gerenciamento de bancos de dados e sempre foi uma prioridade para o Banco de Dados SQL do Azure. O Banco de Dados SQL do Azure dá suporte à segurança de conexão com regras de firewall e criptografia da conexão. Ele dá suporte à autenticação com nome de usuário e senha e a Autenticação do Azure Active Directory, que usa identidades gerenciadas pelo Azure Active Directory. A autorização usa o controle de acesso baseado em função.

Banco de dados do SQL Azure oferece suporte à criptografia executando criptografia em tempo real e a descriptografia de bancos de dados, backups associados e arquivos de log de transações em repouso sem exigir alterações toohello aplicativo.

A Microsoft fornece maneiras adicionais tooencrypt dados da empresa:

-   Nível de célula colunas específicas de tooencrypt de criptografia ou até mesmo células de dados com diferentes chaves de criptografia.
-   Se você precisar de um Módulo de Segurança de Hardware ou do gerenciamento central da hierarquia de chaves de criptografia, considere o uso do Azure Key Vault com o SQL Server em uma VM do Azure.
-   Sempre criptografado (atualmente na visualização) torna tooapplications transparente de criptografia e permite que os clientes tooencrypt os dados confidenciais em aplicativos de cliente sem compartilhar as chaves de criptografia de saudação com banco de dados SQL.

Auditoria de banco de dados SQL do Azure permite que as empresas toorecord eventos tooan auditoria logon armazenamento do Azure. Auditoria de banco de dados SQL também se integra com análises e relatórios do Microsoft Power BI toofacilitate drill-down.

 Bancos de dados do SQL Azure podem ser totalmente protegido toosatisfy mais normas ou requisitos de segurança, como HIPAA, ISO 27001/27002 e PCI DSS nível 1, entre outros. Uma lista atual das certificações de conformidade de segurança está disponível em Olá [site do Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

Este artigo explica fundamentos de saudação de proteção de bancos de dados SQL do Microsoft Azure para estruturada, tabela e dados relacionais. Em particular, este artigo mostrará uma introdução aos recursos de proteção de dados, de controle de acesso e de monitoramento proativo.

Este artigo de visão geral de segurança de banco de dados do Azure enfoca Olá áreas a seguir:

-   Proteger dados
-   Controle de acesso
-   Monitoramento proativo
-   Gerenciamento de segurança centralizado
-   Azure Marketplace

## <a name="protect-data"></a>Proteger dados

O Banco de Dados SQL protege os dados fornecendo criptografia de dados em movimento usando o [protocolo TLS](https://support.microsoft.com/kb/3135244), para dados em repouso usando a [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) e para dados em uso usando o [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx).

Nesta seção, vamos falar sobre:

-   Criptografia em movimento
-   Criptografia em repouso
-   Criptografia em uso (Cliente)

Para outra maneiras tooencrypt seus dados, considere:

-   [Criptografia em nível de célula](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colunas específicas ou mesmo células de dados com diferentes chaves de criptografia.
-   Se você precisar de um Módulo de Segurança de Hardware ou do gerenciamento central de sua hierarquia de chaves de criptografia, considere o uso do [cofre da chave do Azure com o SQL Server em uma VM do Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Criptografia em movimento

Um problema comum para todos os aplicativos cliente/servidor é necessário Olá privacidade como movem dados em redes públicas e privadas. Se mover em uma rede de dados não são criptografados, há possibilidade de saudação que podem ser capturado e roubado por usuários não autorizados. Ao lidar com os serviços de banco de dados, você precisa toomake-se de que os dados são criptografados entre Olá banco de dados cliente e servidor, bem como entre servidores de banco de dados que se comunicam entre si e com aplicativos de camada intermediária.

Um problema ao administrar uma rede é proteger os dados que estão sendo enviados entre aplicativos em uma rede não confiável. Você pode usar [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate servidores e clientes e usá-lo tooencrypt mensagens entre partes Olá autenticado.

No processo de autenticação hello, um cliente TLS/SSL envia um servidor TLS/SSL tooa e servidor de saudação responde com informações de saudação servidor Olá precisa tooauthenticate em si. saudação de cliente e servidor executam uma troca adicional de chaves de sessão e Olá extremidades da caixa de diálogo de autenticação. Quando a autenticação é concluída, comunicação segura SSL pode começar entre o servidor de saudação e cliente de saudação usando chaves de criptografia simétrica de saudação que são estabelecidas durante o processo de autenticação hello.

Todas as conexões tooAzure banco de dados SQL exigir criptografia SSL/TLS () em todas as vezes enquanto os dados são tooand "em trânsito" do banco de dados de saudação. O SQL Azure usa os clientes e servidores de tooauthenticate TLS/SSL e use-a como tooencrypt mensagens entre partes Olá autenticado. Na cadeia de caracteres de conexão do seu aplicativo, você deve especificar a conexão de saudação tooencrypt parâmetros e não tootrust Olá certificado do servidor (Isso é feito para você se você copiar a cadeia de conexão sem Olá Portal clássico do Azure), Olá caso contrário, a conexão será Não verificar a identidade de saudação do servidor de saudação e estará suscetíveis ataques de muito "man-in-the-middle". Para hello driver ADO.NET, por exemplo, esses parâmetros de cadeia de caracteres de conexão Encrypt = True e TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Criptografia em repouso
Você pode tomar várias precauções toohelp Olá seguro banco de dados, como a criação de um sistema seguro, criptografando ativos confidenciais e criando um firewall em torno dos servidores de banco de dados de saudação. No entanto, em um cenário em que a mídia física hello (como unidades ou fitas de backup) é roubada, um terceiro mal-intencionado pode apenas restaurar ou anexar o banco de dados de saudação e procurar dados saudação.

Uma solução tooencrypt Olá contém dados confidenciais no banco de dados de saudação e protege as chaves de hello são usadas tooencrypt Olá dados com um certificado. Isso impede que alguém sem as chaves de saudação usando dados hello, mas esse tipo de proteção deve ser planejado.

toosolve dar suporte a esse problema, o SQL Server e SQL Azure [criptografia de dados transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). A TDE criptografa os arquivos de dados do SQL Server e do Banco de Dados SQL do Azure, conhecidos como dados de criptografia em repouso.

Criptografia de dados transparente de banco de dados SQL do Azure ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de banco de dados hello, backups associados e arquivos de log de transações em repouso sem exigir alterações aplicativo de toohello.  

Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica. No banco de dados SQL, a chave de criptografia de banco de dados de saudação é protegido por um certificado de servidor interno. certificado de saudação do servidor interno é exclusivo para cada servidor de banco de dados SQL.

Se um banco de dados estiver em uma relação de GeoDR, ele será protegido por outra chave em cada servidor. Se dois bancos de dados são conectado toohello mesmo servidor, eles compartilham Olá mesmo certificado interno. A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias. Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Criptografia em uso (cliente)

A maioria das violações de dados envolvem o roubo de saudação de dados essenciais, como números de cartão de crédito ou informações de identificação pessoal. Bancos de dados podem ser um tesouro escondido de informações confidenciais. Eles podem conter dados pessoais dos clientes, informações confidenciais sobre a concorrência e propriedade intelectual. Dados perdidos ou roubados, especialmente dados do cliente, podem resultar em danos à marca, desvantagem competitiva e multas graves – até mesmo processos judiciais.

![Always Encrypted](./media/azure-databse-security-overview/azure-database-fig1.png)

[Sempre criptografado](https://msdn.microsoft.com/library/mt163865.aspx) é um recurso projetado tooprotect dados confidenciais, como números de cartão de crédito ou de identificação Nacional (por exemplo, números de previdência social), armazenado em bancos de dados do banco de dados SQL ou SQL Server. Sempre criptografado permite que os clientes tooencrypt os dados confidenciais em aplicativos de cliente e nunca revele toohello chaves de criptografia Olá mecanismo de banco de dados (banco de dados SQL ou SQL Server).

Sempre criptografado fornece uma separação entre aqueles que possuem dados saudação (e podem exibi-lo) e aqueles que gerenciam dados de saudação (mas não devem ter acesso). Ao garantir que os administradores de banco de dados local, operadores de banco de dados em nuvem ou outros com altos privilégios, mas os usuários não autorizados, não é possível acessar dados criptografado de saudação,

Além disso, sempre criptografado torna tooapplications transparente de criptografia. Um driver habilitado para sempre criptografado instalado no computador do cliente Olá para que pode criptografar e descriptografar dados confidenciais no aplicativo de cliente hello automaticamente. Olá driver criptografa dados Olá colunas confidenciais antes de passar Olá dados toohello mecanismo de banco de dados e reconfigura automaticamente as consultas para que o aplicativo de toohello hello semântica são preservados. Da mesma forma, o driver Olá transparente descriptografa os dados armazenados em colunas de banco de dados criptografados contidas nos resultados da consulta.

## <a name="access-control"></a>Controle de acesso
tooprovide segurança, o banco de dados SQL controla o acesso com regras de firewall limitando conectividade por endereço IP, os mecanismos de autenticação que requerem usuários tooprove sua identidade e mecanismos de autorização, limitando os usuários toospecific ações e dados.

### <a name="database-access"></a>Acesso ao banco de dados

Proteção de dados começa com controle de acesso tooyour dados. Olá datacenter hospedar seus dados gerencia o acesso físico, enquanto você pode configurar a segurança toomanage firewall na camada de rede hello. Você também pode controlar o acesso, configurar logons para autenticação e definir permissões para funções de servidor e de banco de dados.

Nesta seção, vamos falar sobre:

-   Firewall e regras de firewall
-   Autenticação
-   Autorização

#### <a name="firewall-and-firewall-rules"></a>Firewall e regras de firewall

O Banco de Dados SQL do Microsoft Azure fornece um serviço de banco de dados relacional para o Azure e outros aplicativos baseados na Internet. toohelp proteger seus dados, firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede acesso toodatabases com base em Olá endereços IP de cada solicitação de origem. Para saber mais, veja [Visão geral de regras de firewall do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Olá [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/) serviço está disponível somente pela porta TCP 1433. tooaccess um banco de dados SQL do seu computador, verifique se o firewall do computador cliente permite a comunicação TCP de saída na porta TCP 1433. Se não for necessário a outros aplicativos, bloqueie as conexões de entrada na porta TCP 1433.

#### <a name="authentication"></a>Autenticação

Autenticação do banco de dados SQL refere-se toohow provar sua identidade ao conectar-se o banco de dados toohello. O Banco de Dados SQL dá suporte a dois tipos de autenticação:

-   **Autenticação do SQL:** uma conta de logon único é criada quando é criada uma instância lógica do SQL, chamado hello conta de assinante do banco de dados SQL. Essa conta é conectada usando a [autenticação do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nome de usuário e senha). Essa conta é que um administrador na instância de servidor lógico hello e em todos os bancos de dados do usuário conectado toothat instância. permissões de saudação do hello conta do assinante não podem ser restritas. Só pode existir uma dessas contas.
-   **Azure autenticação do Active Directory:** [autenticação do Active Directory do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) é um mecanismo de conexão tooMicrosoft banco de dados do SQL Azure e SQL Data Warehouse usando as identidades no Active Directory do Azure ( AD do Azure). Isso permite que você toocentrally gerenciar identidades de usuários de banco de dados.

![Autenticação](./media/azure-databse-security-overview/azure-database-fig2.png)

 As vantagens da autenticação do Azure Active Directory incluem:
  - Ele fornece uma autenticação de servidor tooSQL alternativo.
  - Ele também ajuda a interromper a proliferação de saudação de identidades de usuário entre os servidores de banco de dados e permite a rotação de senha em um único lugar.
  - Gerencie permissões de banco de dados usando grupos externos (Azure Active Directory).
  - Pode eliminar o armazenamento de senhas, permitindo a autenticação integrada do Windows e outras formas de autenticação às quais o Active Directory do Azure dá suporte.

#### <a name="authorization"></a>Autorização
[Autorização](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) toowhat de refere-se um usuário pode fazer em um banco de dados do SQL Azure, e isso é controlado pelo banco de dados da sua conta de usuário [associações de função](https://msdn.microsoft.com/library/ms189121) e [permissões no nível do objeto](https://msdn.microsoft.com/library/ms191291.aspx). A autorização é o processo de saudação de determinar quais recursos podem ser protegidos pode acessar uma entidade de segurança e quais operações são permitidas para esses recursos.

### <a name="application-access"></a>Acesso a aplicativos

Nesta seção, vamos falar sobre:

-   Mascaramento de dados dinâmicos
-   Segurança em nível de linha

#### <a name="dynamic-data-masking"></a>Mascaramento de dados dinâmicos
Um representante do serviço em um call center pode identificar os chamadores usando vários dígitos de seu número de previdência social ou número de cartão de crédito, mas esses dados itens não devem ser totalmente expostos toohello representante.

Uma regra de mascaramento pode ser definida se mascarar todos exceto Olá últimos quatro dígitos de qualquer número de previdência social ou número de cartão de crédito no conjunto de resultados de saudação de qualquer consulta.

![Mascaramento de dados dinâmicos](./media/azure-databse-security-overview/azure-database-fig3.png)

Como outro exemplo, uma máscara de dados apropriado pode ser definido tooprotect dados de informações de identificação pessoal (PII), para que um desenvolvedor pode consultar os ambientes de produção para fins de solução de problemas sem violar os regulamentos de conformidade.

[Banco de dados dinâmico mascaramento de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon. Mascaramento de dados dinâmicos é suportado para a versão V12 de saudação do banco de dados do SQL Azure.

[Mascaramento de dados dinâmicos](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) ajuda a impedir que os dados de toosensitive de acesso não autorizado, permitindo que você toodesignate quanto da saudação dados confidenciais tooreveal com impacto mínimo sobre a camada de aplicativo hello. É um recurso de segurança baseado em políticas que oculta os dados confidenciais de saudação no conjunto de resultados de saudação de uma consulta em relação aos campos do banco de dados designados, enquanto Olá dados no banco de dados de saudação não são alterados.


> [!Note]
> Mascaramento de dados dinâmicos pode ser configurado por Olá administrador de banco de dados, administrador do servidor ou funções de diretor de segurança.

#### <a name="row-level-security"></a>Segurança em nível de linha
Outro requisito de segurança comum para bancos de dados multilocatários é a [Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131.aspx). Esse recurso permite que você toocontrol toorows de acesso em uma tabela de banco de dados com base em características de saudação do usuário Olá executando uma consulta (por exemplo, grupo associação ou contexto de execução).

![Segurança em nível de linha](./media/azure-databse-security-overview/azure-database-fig4.png)

lógica de restrição de acesso de saudação é localizado na camada de banco de dados de saudação em vez de longe dos dados de saudação em outra camada de aplicativo. sistema de banco de dados de saudação aplica restrições de acesso de saudação toda vez que acesso a dados é tentado em qualquer nível. Isso torna o sistema de segurança mais robusto e confiável, reduzindo a área de superfície de saudação do seu sistema de segurança.

A segurança em nível de linha introduz o controle de acesso baseado em predicado. Ele apresenta uma avaliação centralizada, flexível e baseada em predicado que pode levar em consideração metadados ou quaisquer outros critérios Olá administrador determina conforme apropriada. predicado de saudação é usado como um critério toodetermine ou não usuário Olá tem Olá apropriado acessar toohello dados com base em atributos de usuário. O controle de acesso baseado em rótulo pode ser implementado usando o controle de acesso baseado em predicado.

## <a name="proactive-monitoring"></a>Monitoramento proativo
O Banco de Dados SQL protege os dados fornecendo funcionalidades de **auditoria** e **detecção de ameaças**.

### <a name="auditing"></a>Auditoria
Auditoria de banco de dados SQL aumenta sua capacidade toogain percepção eventos e as alterações que ocorrem no banco de dados do hello, incluindo atualizações e consultas em dados hello.

[Auditoria de banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure. A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança. A auditoria permite e facilita a padrões de toocompliance aderência mas não garante conformidade.

A auditoria de Banco de Dados SQL permite:

-   **Retenha** uma trilha de auditoria dos eventos selecionados. Você pode definir categorias de banco de dados ações toobe auditado.
-   **Relate** sobre a atividade do banco de dados. Você pode usar relatórios pré-configurados e um tooget painel iniciada rapidamente com a atividade e o relatório de eventos.
-   **Analise** relatórios. Encontrar eventos suspeitos, atividades incomuns e tendências.

Há dois métodos de Auditoria:

-   **Auditoria de blob** -os logs são gravados tooAzure armazenamento de Blob. Esse é um método de auditoria mais recente, que fornece desempenho maior, dá suporte à auditoria do nível de objeto de granularidade mais alta e é mais econômico.
-   **Auditoria de tabela** -tooAzure o armazenamento de tabela os logs são gravados.

### <a name="threat-detection"></a>Detecção de ameaças
A [detecção de ameaças do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) detecta atividades suspeitas que indicam possíveis ameaças à segurança. A detecção de ameaças permite toorespond toosuspicious eventos no banco de dados do hello como inclusões de SQL, conforme elas ocorrem. Ele fornece alertas e permite o uso de saudação de auditoria do banco de dados SQL Azure tooexplore eventos suspeitos hello.

![Detecção de ameaças](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Por exemplo, injeção de SQL é um Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados. Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, serem violados ou modificar dados no banco de dados de saudação.

Os agentes de segurança ou outros administradores designados podem obter uma notificação imediata sobre atividades suspeitas de banco de dados conforme eles ocorrem. Cada notificação fornece detalhes de atividade suspeita hello e recomenda como toofurther investigar e reduzir a ameaça de saudação.        

## <a name="centralized-security-management"></a>Gerenciamento de segurança centralizado

[Central de segurança do Azure](https://azure.microsoft.com/documentation/services/security-center/) ajuda a evitar, detectar e responder toothreats. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

[Central de segurança](https://docs.microsoft.com/azure/security-center/security-center-sql-database) ajuda a proteger dados no banco de dados SQL, fornecendo a visibilidade de segurança de saudação de todos os servidores e bancos de dados. Com a Central de Segurança, você pode:

-   Definir políticas de criptografia e auditoria do Banco de Dados SQL.
-   Monitorar a segurança de saudação de recursos de banco de dados SQL em todas as suas assinaturas.
-   Identifique e corrija rapidamente problemas de segurança.
-   Integre os alertas da [detecção de ameaças do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   A Central de segurança dá suporte ao acesso baseado em função.

## <a name="azure-marketplace"></a>Azure Marketplace

Hello Azure Marketplace é um mercado de aplicativos e serviços online que permite que empresas emergentes e software independentes (ISVs) fornecedores toooffer seus clientes de tooAzure soluções em torno de Olá, mundo.
Hello Azure Marketplace combina ecossistemas de parceiro do Microsoft Azure em uma única plataforma unificada toobetter atende nossos clientes e parceiros. Clique em [aqui](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance disponível no local do Azure do mercado de produtos de segurança de banco de dados.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre como [Proteger o Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Saiba mais sobre a [Central de Segurança do Azure e o serviço Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- toolearn mais sobre a detecção de ameaças, consulte [detecção de ameaças do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- mais, consulte toolearn [desempenho de banco de dados SQL melhorar](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
