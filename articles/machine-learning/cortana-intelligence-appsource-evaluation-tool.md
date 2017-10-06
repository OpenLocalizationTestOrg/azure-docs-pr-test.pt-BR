---
title: "ferramenta de avaliação de solução de inteligência aaaCortana | Microsoft Docs"
description: "Como Microsoft Partner, aqui estão todas as etapas de saudação precisar toofollow toopublish sua tooAppSource de solução de inteligência do Cortana."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Ferramenta de avaliação da solução do Cortana Intelligence
## <a name="overview"></a>Visão geral
Você pode usar o hello tooassess de ferramenta de avaliação de solução de inteligência Cortana suas soluções de análise avançada quanto à conformidade com as práticas recomendadas da Microsoft. A Microsoft está toowork felizes com nossos parceiros (ISVs / SIs) tooprovide soluções de alta qualidade para clientes, revendedores e implementação. Este guia de percorrer o processo de saudação do usando a ferramenta de avaliação de solução de saudação com sua solução e descrevem Olá práticas recomendadas em verificações de.

## <a name="getting-started"></a>Introdução
Por favor, [baixar](https://aka.ms/aa-evaluation-tool-download) e instalar a ferramenta de avaliação de solução de inteligência Cortana hello.

Pré-requisitos:
- Windows 10: [Site oficial para o Windows 10](https://www.microsoft.com/en-us/windows)
- Azure Powershell: [Instale e configure o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).

## <a name="identifying-your-app"></a>Identificando seu aplicativo
Após a conclusão da instalação, abra a ferramenta de saudação e comece sua primeira avaliação.

![Abra a ferramenta de avaliação](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Forneça informações de identificação sobre sua solução.

![Conecte a assinatura do Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Conecte-se tooyour assinatura do Azure e fornecer Olá grupo de recursos que contém seu aplicativo.

![Selecionar recursos](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Depois que o grupo de recursos de saudação foi carregado, selecione recursos Olá que estão incluídos em sua solução e identificam a acessibilidade de saudação de quaisquer recursos de dados como:
- Ingestão
- Consumo
- Interna

Usamos essas informações toobetter entender como sua solução utiliza vários componentes e tooensure voltadas para o usuário componentes são consistentes com as práticas recomendadas.

### <a name="ingestion"></a>Ingestão
Nesse caso, a inclusão significa qualquer fonte de dados que são toopull usado nos dados da solução Olá externa ou que todos os serviços fora Olá solução usam toopush dados nele.

### <a name="consumption"></a>Consumo
Nesse caso, o consumo significa qualquer conjuntos de dados que são usados toopush dados tooend usuários, direta ou indiretamente. Por exemplo:
- Conjuntos de dados usados em consultas diretas da PowerBI.
- Conjuntos de dados consultados em um aplicativo Web.

>[!NOTE]
Caso um recurso específico seja usado tanto para a ingestão quanto para o consumo, por favor, escolha **Consumo**.

### <a name="internal"></a>Interna
Use o interno para quaisquer recursos de dados que sejam usados somente no processo de aplicativo interno.

Em seguida, você estará tooprovide solicitadas de credenciais válidas para qualquer banco de dados especificado na etapa anterior hello:

![Defina os pré-requisitos para a realização do teste](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Casos de testes referentes à solução
ferramenta de solução de saudação executará um conjunto de testes automatizados em sua solução.

![Defina a execução do teste](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Após a conclusão dos testes hello, será solicitado que tooprovide uma explicação ou justificação por que sua solução não está de acordo com o requisito de saudação.

![Fornecer uma justificação de negócios](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Por exemplo, se sua solução publica tooAzure SQL DW, avaliação de saudação testes exigem tooalso você publicar tooAzure Analysis Services. 

Sua solução pode usar máquinas virtuais IaaS executando o SQL Server Analysis Services em vez do Azure Analysis Services. Isso seria um motivo aceitável para falha de teste de saudação.
## <a name="packaging-your-evaluation-results"></a>Guardando os resultados de avaliação
Depois de concluir os casos de teste hello, seu pacote de avaliação será arquivo zip de tooa exportado e você deverá tooprovide comentários na ferramenta de avaliação de saudação. 

É necessário tooshare esse teste resultados arquivo zip com a Microsoft para sua toobe solução avaliada antes de obter aprovação toobe adicionado tooAppSource

![Avalie a ferramenta de avaliação](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Acima da seção deste artigo abrange vários recursos da ferramenta hello, agora, vamos rever tipos de práticas recomendadas que essa ferramenta é avaliada.

## <a name="security-evaluation-considerations"></a>Considerações sobre a avaliação da segurança
### <a name="databases-should-use-azure-active-directory-authentication"></a>As bases de dados devem usar a autenticação do Azure Active Directory
Recursos SQL Azure ou Azure SQL DW Olá sloution devem ser habilitados com a autenticação do Azure Active Directory (AAD). AAD fornece um único local toomanage todas as identidades e funções.

| Para saber mais sobre | Consulte este artigo |
| --- | --- |
| AAD com Banco de Dados SQL e SQL Data Warehouse | [Use a autenticação do Azure Active Directory com o banco de dados SQL ou com o SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Configure e gerencie a AAD | [Configurar e gerenciar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Autenticação dos Aplicativos Web do Azure | [Autenticação e autorização no Serviço de Aplicativo do Azure](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Configure os aplicativos Web com a AAD | [Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Active Directory do Azure](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Conjuntos de dados acessível tooend-usuários devem dar suporte a controle de acesso baseado em função
Ao executar a ferramenta de avaliação de saudação, você será solicitado a toospecify qualquer relatório ou a publicação de recursos. Assume-se que esses recursos servem para serem acessados pelos usuários finais, não pelos desenvolvedores. Esses recursos devem ser fornecem controle de acesso baseado em função (RBAC) em ordem tooensure que os usuários finais são apenas capaz de tooaccess autorizado a dados.

Especificamente, qualquer Olá recursos do Azure a seguir pode ser configurado com RBAC e são considerados aceitáveis:
- Proteger HDInsight, consulte [uma segurança tooHadoop de Introdução com clusters de HDInsight ingressado no domínio](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL, consulte [ autenticação da AAD com Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)
- Azure Analysis Services, consulte [ a gestão das funções e usuários da base de dados para os Serviços de Análise do Azure](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users)
- SQL Data Warehouse do Azure (Fique atento a isso porque o SQL DW suporta o RBAC, não é recomendado para o acesso direto do usuário final.)

Se você estiver usando um tipo de recurso diferente que dá suporte ao RBAC, especifique que na justificativa de caso de teste de saudação.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store deve usar uma criptografia em repouso
Azure Data Lake Store (ADLS) suporta uma criptografia em repouso padrão usando chaves de criptografia gerenciadas do ADLS. Você também pode configurar a criptografia usando o Azure Key Vault.

Para mais informações sobre as configurações específicas de criptografia do ADLS, [crie uma conta do Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>O SQL Azure e o SQL Data Warehouse do Azure devem usar a criptografia
Tanto o SQL do Azure e quanto o Azure SQL DW oferecem o suporte Transparent Data Encryption (TDE), que fornece criptografia e descriptografia em tempo real tanto nos dados quanto nos arquivos de log.

| Para saber mais sobre | Consulte este artigo |
| --- | --- |
| Transparent Data Encryption (TDE) | [Transparent Data Encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| SQL Data Warehouse do Azure com o TDE | [ Criptografia do SQL Data Warehouse TDE TSQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Configure o SQL do Azure com TDE | [Transparent Data Encryption com o Banco de Dados SQL do Azure](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Configure o SQL Azure sempre com Always Encrypted | [O banco de dados SQL Always Encrypted Azure Key Vault](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Além disso tooTDE, SQL Azure também oferece suporte ao sempre criptografado, uma nova tecnologia de criptografia de dados que garante que os dados são criptografados não apenas em repouso e durante a movimentação entre cliente e servidor, mas também ao dados está em uso ao executar comandos no servidor de saudação.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Todas as máquinas virtuais devem ser implantados de saudação do Azure Marketplace
Em ordem tooprovide um nível consistente de segurança em AppSource, é necessário que todas as máquinas virtuais implantadas como parte de uma solução de inteligência Cortana certificadas e publicadas no hello Azure Marketplace.

saudação de toosearch lista atual de imagens do Azure Marketplace, consulte [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Para obter informações sobre como toopublish uma máquina virtual da imagem para o Azure Marketplace, consulte [guia toocreate uma imagem de máquina virtual para hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Considerações sobre a avaliação de escalabilidade
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Soluções Cortana Intelligence devem incluir uma plataforma Big Data escalonável
Soluções de inteligência de Cortana devem ser dimensionado toovery tamanhos de dados grandes. No Azure, isso significa que eles devem incluir uma das duas plataformas de dados de escala de petabytes hello:
- Repositório Azure Data Lake
- SQL Data Warehouse do Azure

Se sua solução não exigir suporte para esses tamanhos de dados ou se você estiver usando uma plataforma de dados alternativos, explique isso em justificativa de caso de teste de saudação.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Soluções Cortana Intelligence devem incluir ambientes de dados dedicados à ingestão
Soluções Cortana Intelligence devem evitar a inserção direta de dados nas fontes de dados relacionais. Ao invés disso, os dados brutos devem ser armazenados em um ambiente não estruturado, com inserções/atualizações idempotentes em quaisquer armazenamentos relacionais usando o Azure Data Factory.

Para mais informações sobre os dados da Azure Data Factory, [Tutorial: crie um pipeline com uma atividade de Cópia usando um estúdio visual](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>O SQL Data Warehouse do Azure deve usar o PolyBase para a ingestão de dados
O SQL DW Azure suporta o PolyBase para a ingestão de dados altamente escalonável e paralela. O PolyBase permite que você tooissue consultas Azure SQL DW toouse conjuntos de dados externos armazenados no armazenamento de BLOBs do Azure ou no repositório Azure Data Lake. Isso fornece desempenho superior tooalternative métodos de atualizações em massa.

Para obter instruções sobre como começar com a PolyBase e o SQL DW da Azure, consulte [os dados de carga com a PolyBase no SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Para saber mais sobre as melhores práticas com a PolyBase e com o SQL DW da Azure, consulte [Guia para o uso da PolyBase no SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Considerações sobre a avaliação da disponibilidade

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Os usuários tooend acessível de conjuntos de dados devem oferecer suporte a um grande volume de usuários simultâneos
Ao executar a ferramenta de avaliação de saudação, você será solicitado a toospecify qualquer relatório ou a publicação de recursos. Assume-se que esses recursos servem para serem acessados pelos usuários finais, não pelos desenvolvedores. Esses recursos devem suportar um número médio/grande de usuários ao mesmo tempo.

Especificamente, o Azure SQL Data Warehouse não devem ser usuários de tooend disponíveis de origem de dados único hello. Se o Azure SQL DW é fornecido como um recurso para usuários avançados, Azure Analysis Services devem ser feito para usuários tootypical disponíveis.

Para saber mais sobre os limites de simultaneidade da SQL DW do Azure, consulte [Gerenciamento e carga de trabalho no SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Para mais informações sobre Azure Analysis Services, consulte [Visão geral do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Os recursos do SQL do Azure devem ter uma réplica somente leitura para failover
Bancos de dados SQL do Azure oferecem suporte a instância secundária de tooa de replicação geográfica. Esta instância, em seguida, pode ser usada como um aplicativo de alta disponibilidade de tooprovide de instância de failover.

Para saber mais sobre a replicação geográfica para bancos de dados do SQL Azure, consulte [Visão geral da replicação Geográfica do banco de dados SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Para obter instruções sobre como replicação geográfica tooconfigure para SQL Azure, consulte [configurar replicação geográfica ativa para banco de dados SQL Azure com o Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>O SQL Data Warehouse do Azure deverá ter backups com redundância geográfica habilitados
Azure SQL DW dá suporte a armazenamento toogeo redundantes de backups diários. Essa replicação geográfica garante que você possa restaurar o data warehouse de saudação mesmo em situações em que você não pode acessar os instantâneos armazenados em sua região primária. Esse recurso é ativado como padrão e não deve ser desabilitado para as soluções Cortana Intelligence.

Para ter mais informações sobre os backups e a restauração do SQL DW do Azure, consulte aqui [Backups do SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>As máquinas virtuais devem ser configuradas com conjuntos de disponibilidade
Máquinas virtuais do Azure deve ser configuradas em conjuntos de disponibilidade em ordem toominimize Olá impacto manutenções planejadas e não planejadas.

Para obter mais informações sobre a disponibilidade da máquina virtual do Azure, consulte [gerenciar Olá disponibilidade de máquinas virtuais do Windows no Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Outras considerações sobre a avaliação
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Os aplicativos da Cortana Intelligence devem usar uma ferramenta de orquestração de dados
Usar uma única ferramenta para gerenciar e planejar o movimento e a transformação dos dados garante a consistência em torno dos dados críticos da missão. Fornece uma lógica clara em torno da lógica de repetição, gestão de dependência, alerta/registro, etc. Recomendamos o uso de saudação do [do Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) de orquestração de dados no Azure.

Se você estiver usando uma ferramenta diferente do Azure Data Factory para orquestração, descreva qual ferramenta ou ferramentas que você está usando.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Os modelos da Azure Machine Learning devem ser requalificados usando Azure Data Factory
Aprendizado de máquina do Azure (AzureML) fornece ferramentas de fácil toouse para criação de saudação e implantação de modelagem de previsão e pipelines de aprendizado de máquina. No entanto, é importante que as implantações de produção desses modelos AzureML não se baseia em um único conjunto de dados fixado, mas em vez disso, se adapta toohello mudanças na dinâmica de fenômenos do mundo real.

Para saber mais sobre como criar reciclagem de serviços Web em AzureML, consulte [Recicle Machine Learning de forma programada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Para obter mais informações sobre como automatizar o processo de treinamento de modelo Olá utilizando a fábrica de dados do Azure, consulte [modelos de atualização de aprendizado de máquina do Azure usando a atividade de atualização de recurso](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Documentação existente
[Microsoft Azure Certified toogrow seu negócio de nuvem](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Certified para Cortana Intelligence](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

