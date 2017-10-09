---
title: "Considerações de aaaSecurity para movimentação de dados no Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre como proteger a movimentação de dados no Azure Data Factory."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory – Considerações sobre segurança para movimentação de dados
## <a name="introduction"></a>Introdução
Este artigo descreve a infraestrutura de segurança básico que os serviços de movimentação de dados no Azure Data Factory usam toosecure seus dados. Os recursos de gerenciamento do Azure Data Factory se baseiam na infraestrutura de segurança do Azure e usam todas as medidas de segurança possíveis oferecidas pelo Azure.

Em uma solução de Data Factory, você cria um ou mais [pipelines](data-factory-create-pipelines.md)de dados. Um pipeline é um agrupamento lógico de atividades que juntas executam uma tarefa. Desses pipelines residam na região Olá onde a fábrica de dados Olá foi criada. 

Mesmo que a fábrica de dados está disponível somente em **Oeste dos EUA**, **Leste dos EUA**, e **Norte da Europa** regiões, o serviço de movimentação de dados hello está disponível [globalmente no várias regiões](data-factory-data-movement-activities.md#global). Fábrica de dados garante que os dados não deixar uma área geográfica / região, a menos que você instruir explicitamente Olá serviço toouse uma região alternativa se o serviço de movimentação de dados Olá não for implantado ainda toothat região. 

O Azure Data Factory em si não armazena nenhum dado, exceto as credenciais do serviço vinculado de armazenamentos de dados em nuvem, que são criptografadas com o uso de certificados. Ele permite que você crie fluxos de trabalho controlados por dados tooorchestrate movimentação de dados entre [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) e processamento de dados usando [serviços de computação](data-factory-compute-linked-services.md) em outras regiões ou em um local ambiente. Ele também permite que você muito[monitorar e gerenciar fluxos de trabalho](data-factory-monitor-manage-pipelines.md) usando programático e mecanismos de interface do usuário.

A movimentação de dados com o uso do Azure Data Factory foi **certificada** na:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Se você estiver interessado em como o Azure protege sua própria infraestrutura e de conformidade do Azure, visite Olá [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

Neste artigo, vamos examinar considerações de segurança no hello dois cenários de movimentação de dados a seguir: 

- **Cenário de nuvem** – neste cenário, a origem e o destino são publicamente acessíveis pela Internet. Eles incluem serviços de armazenamento em nuvem gerenciados como Armazenamento do Azure, SQL Data Warehouse do Azure, Banco de Dados SQL do Azure, Azure Data Lake Store, Amazon S3, Amazon Redshift, serviços SaaS como Salesforce e protocolos da Web como FTP e OData. Encontre uma lista completa de fontes de dados com suporte [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- **Cenário híbrido**- neste cenário, a origem ou destino está atrás de um firewall ou dentro de um local corporativo hello ou rede de dados repositório está em uma rede privada virtual (geralmente origem Olá) de rede e não está acessível publicamente . Os servidores de banco de dados hospedados em máquinas virtuais também se enquadram nesse cenário.

## <a name="cloud-scenarios"></a>Cenários de nuvem
###<a name="securing-data-store-credentials"></a>Protegendo as credenciais do armazenamento de dados
O Azure Data Factory protege suas credenciais do armazenamento de dados **criptografando-as** usando **certificados gerenciados pela Microsoft**. Esses certificados são trocados a cada **dois anos** (que inclui a renovação do certificado e a migração de credenciais). Essas credenciais criptografadas são armazenadas com segurança em um **Armazenamento do Azure gerenciado pelos serviços de gerenciamento do Azure Data Factory**. Para obter mais informações sobre a segurança do Armazenamento do Azure, consulte [Visão geral de segurança do Armazenamento do Azure](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Criptografia de dados em trânsito
Se o repositório de dados de nuvem Olá dá suporte a HTTPS ou TLS, todos os dados são transferidos entre serviços de movimentação de dados na fábrica de dados e um repositório de dados de nuvem são via canal seguro, HTTPS ou TLS.

> [!NOTE]
> Todas as conexões muito**banco de dados do SQL Azure** e **Azure SQL Data Warehouse** sempre exigir criptografia (SSL/TLS), enquanto os dados estão em trânsito tooand do banco de dados de saudação. Ao criar um pipeline usando um editor de JSON, adicionar Olá **criptografia** propriedade e defini-lo muito**true** em Olá **cadeia de caracteres de conexão**. Quando você usa Olá [Assistente para cópia de](data-factory-azure-copy-wizard.md), Assistente de saudação define essa propriedade por padrão. Para **armazenamento do Azure**, você pode usar **HTTPS** na cadeia de caracteres de conexão de saudação.

### <a name="data-encryption-at-rest"></a>Criptografia de dados em repouso
Alguns armazenamentos de dados dão suporte à criptografia de dados em repouso. Sugerimos que você habilite o mecanismo de criptografia de dados nesses armazenamentos de dados. 

#### <a name="azure-sql-data-warehouse"></a>SQL Data Warehouse do Azure
Criptografia de dados transparente (TDE) no Data warehouse do SQL Azure ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia dos dados em repouso. Esse comportamento é transparente toohello cliente. Para obter mais informações, consulte [Proteger um banco de dados no SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
Banco de dados SQL do Azure também oferece suporte a criptografia de dados transparente (TDE), que ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de dados saudação sem a necessidade de alterações toohello aplicativo. Esse comportamento é transparente toohello cliente. Para obter mais informações, consulte [Transparent Data Encryption com o Banco de Dados SQL do Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Repositório Azure Data Lake
Repositório Data Lake do Azure também fornece criptografia de dados armazenados na conta de saudação. Quando habilitada, o repositório Data Lake automaticamente criptografa os dados antes de persistir e descriptografa antes da recuperação, tornando-o cliente toohello transparente acessando dados saudação. Para obter mais informações, consulte [Segurança no Azure Data Lake Store](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Armazenamento de Blobs do Azure e Armazenamento de Tabelas do Azure
Armazenamento de tabela do Azure e armazenamento de Blob do Azure dá suporte à criptografia de serviço de armazenamento (SSE), que criptografa automaticamente os dados antes de persistir toostorage e descriptografa antes da recuperação. Para obter mais informações, consulte [Criptografia de serviço do Armazenamento do Azure para dados em repouso](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
O Amazon S3 dá suporte à criptografia de cliente e de servidor de dados em repouso. Para obter mais informações, consulte [Proteger dados usando a criptografia](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Atualmente, o Data Factory não dá suporte ao Amazon S3 em uma VPC (nuvem privada virtual).

#### <a name="amazon-redshift"></a>Amazon Redshift
O Amazon Redshift dá suporte à criptografia de cluster de dados em repouso. Para obter mais informações, consulte [Criptografia de banco de dados do Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html). Atualmente, o Data Factory não dá suporte ao Amazon Redshift em uma VPC. 

#### <a name="salesforce"></a>Salesforce
O Salesforce dá suporte à Shield Platform Encryption, que permite a criptografia de todos os arquivos, anexos e campos personalizados. Para obter mais informações, consulte [Olá Noções básicas sobre fluxo de autenticação do Web Server OAuth](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Cenários híbridos (usando o Gateway de Gerenciamento de Dados)
Cenários híbridos exigem toobe Data Management Gateway instalado em uma rede local ou em uma rede virtual (Azure) ou uma nuvem privada virtual (Amazon). gateway Olá deve ser capaz de tooaccess armazenamentos de dados locais de saudação. Para obter mais informações sobre o gateway hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md). 

![Canais do Gateway de Gerenciamento de Dados](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Olá **canal do comando** permite a comunicação entre serviços de movimentação de dados na fábrica de dados e o Gateway de gerenciamento de dados. comunicação Olá contém informações relacionadas a atividade de toohello. canal de dados de saudação é usado para transferir dados entre armazenamentos de dados locais e repositórios de dados de nuvem.    

### <a name="on-premises-data-store-credentials"></a>Credenciais do armazenamento de dados local
credenciais de saudação para seus armazenamentos de dados local são armazenadas localmente (não em nuvem Olá). Elas podem ser definidas de três maneiras diferentes. 

- Usando **texto sem formatação** (menos seguro) por HTTPS no Portal do Azure/Assistente de Cópia. Olá credenciais são passadas no gateway do local toohello de texto sem formatação.
- Usando a **biblioteca de Criptografia do JavaScript no Assistente de Cópia**.
- Usando o **aplicativo gerenciador de credenciais baseado em clique único**. Olá clique-quando o aplicativo é executado na máquina de local de saudação que tem acesso toohello gateway e define as credenciais para o repositório de dados hello. Essa opção e hello próxima são Olá opções mais seguras. aplicativo do Gerenciador de credenciais Hello, por padrão, usa a porta Olá 8050 na máquina de saudação com gateway para comunicação segura.  
- Use [AzureRmDataFactoryEncryptValue novo](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) credenciais de tooencrypt de cmdlet do PowerShell. Olá cmdlet usa o certificado de saudação que gateway é configurado toouse tooencrypt Olá credenciais. Você pode usar credenciais Olá criptografado retornadas por este cmdlet e adicioná-lo muito**EncryptedCredential** elemento de saudação **connectionString** no arquivo JSON Olá que você usa com hello [ Novo AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet ou no trecho JSON a saudação em Olá Editor da fábrica de dados no portal de saudação. Clique essa opção e hello-depois de aplicativo são opções mais seguras hello. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Criptografia baseada na biblioteca de criptografia do JavaScript
Você pode criptografar credenciais do repositório de dados usando [biblioteca JavaScript criptografia](https://www.microsoft.com/download/details.aspx?id=52439) de saudação [Assistente para cópia de](data-factory-copy-wizard.md). Quando você seleciona essa opção, Olá Assistente para cópia recupera a chave pública de saudação do gateway e o utiliza tooencrypt Olá credenciais do repositório de dados. credenciais de saudação são descriptografadas pelo computador do gateway hello e protegidas pelo Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Navegadores com suporte:** IE8, IE9, IE10, IE11, Microsoft Edge e últimos navegadores Firefox, Chrome, Opera e Safari. 

#### <a name="click-once-credentials-manager-app"></a>Aplicativo gerenciador de credenciais de clique único
Você pode iniciar Olá clique-uma vez com base de aplicativo do Gerenciador de credenciais do portal do Azure/copiar assistente ao criar pipelines. Este aplicativo garante que as credenciais não são transferidas em texto sem formatação via transmissão hello. Por padrão, ele usa a porta de saudação **8050** na máquina de saudação com gateway para comunicação segura. Se necessário, essa porta pode ser alterada.  
  
![Porta HTTPS para o gateway de saudação](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Atualmente, o Gateway de Gerenciamento de Dados usa um único **certificado**. Esse certificado é criado durante a instalação do gateway hello (aplica-se tooData Gateway de gerenciamento criado após novembro de 2016 e versão 2.4.xxxx.x ou posterior). Você pode substituir esse certificado por seu próprio certificado SSL/TLS. Esse certificado é usado pelo clique Olá-depois que toosecurely de aplicativo do Gerenciador de credenciais se conectar a máquina de gateway toohello para definir as credenciais de repositório de dados. Ele armazena dados de repositório de credenciais com segurança no local usando o Windows hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) na máquina de saudação com o gateway. 

> [!NOTE]
> Os gateways mais antigos que foram instalados antes de novembro de 2016 ou de versão 2.3.xxxx.x continuam toouse credenciais criptografadas e armazenadas na nuvem. Mesmo se você atualizar a versão mais recente do hello gateway toohello, credenciais de saudação não são migrados tooan máquina de local    
  
| Versão do gateway (durante a criação) | Credenciais armazenadas | Criptografia/segurança de credenciais | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | Na nuvem | Criptografado usando o certificado (diferente da saudação usado pelo aplicativo do Gerenciador de credenciais) | 
| > = 2.4.xxxx.x | No local | Protegidas pela DPAPI | 
  

### <a name="encryption-in-transit"></a>Criptografia em trânsito
Todas as transferências de dados são via canal seguro **HTTPS** e **TLS sobre TCP** ataques man-in-the-middle de tooprevent durante a comunicação com os serviços do Azure.
 
Você também pode usar [VPN IPSec](../vpn-gateway/vpn-gateway-about-vpn-devices.md) ou [rota expressa](../expressroute/expressroute-introduction.md) toofurther canal de comunicação seguro Olá entre sua rede local e o Azure.

Rede virtual é uma representação lógica da rede em nuvem hello. Você pode se conectar a uma rede de local tooyour rede virtual do Azure (VNet) com a configuração VPN IPSec (site a site) ou Express Route (emparelhamento privado)       

Olá tabela a seguir resume Olá rede e gateway recomendações de configuração com base em diferentes combinações de locais de origem e destino para a movimentação de dados híbrido.

| Fonte | Destino | Configuração de rede | Instalação do gateway |
| ------ | ----------- | --------------------- | ------------- | 
| Configuração local | Máquinas virtuais e serviços de nuvem implantados em redes virtuais | VPN IPsec (ponto a site ou site a site) | O gateway pode ser instalado localmente ou em uma VM (máquina virtual) do Azure na VNet | 
| Configuração local | Máquinas virtuais e serviços de nuvem implantados em redes virtuais | ExpressRoute (Emparelhamento Privado) | O gateway pode ser instalado localmente ou em uma VM do Azure na VNet | 
| Configuração local | Serviços baseados no Azure que têm um ponto de extremidade público | ExpressRoute (Emparelhamento Público) | O gateway deve ser instalado localmente | 

Olá imagens a seguir mostram o uso de saudação do Gateway de gerenciamento de dados para mover dados entre um banco de dados local e serviços do Azure usando o rota expressa e VPN IPSec (com a rede Virtual):

**ExpressRoute:**
 
![Usar o ExpressRoute com o gateway](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**VPN IPsec:**

![VPN IPsec com gateway](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Configurações de firewall e lista de permissões do endereço IP do gateway

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Requisitos de firewall para a rede local/privada  
Em uma empresa, um **firewall corporativo** é executado no roteador central de saudação da organização hello. E, **firewall do Windows** é executado como um daemon na máquina local hello, no qual Olá gateway está instalado. 

Olá tabela a seguir fornece **a porta de saída** e requisitos de domínio para Olá **firewall corporativo**.

| Nomes de domínio | Portas de saída | Descrição |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Necessário para serviços de movimentação Olá gateway tooconnect toodata na fábrica de dados |
| `*.core.windows.net` | 443 | Usado pelo Olá gateway tooconnect tooAzure conta de armazenamento ao usar o hello [preparados cópia](data-factory-copy-activity-performance.md#staged-copy) recurso. | 
| `*.frontend.clouddatahub.net` | 443 | Exigido pelo Olá gateway tooconnect toohello serviço do Azure Data Factory. | 
| `*.database.windows.net` | 1433   | (OPCIONAL) Necessária quando o destino é o Banco de Dados SQL do Azure/SQL Data Warehouse do Azure. Saudação de uso de preparo cópia recurso toocopy dados tooAzure SQL do Azure/banco de dados SQL Data Warehouse sem abrir a porta 1433 hello. | 
| `*.azuredatalakestore.net` | 443 | (OPCIONAL) Necessária quando o destino é o Azure Data Lake Store | 

> [!NOTE] 
> Você pode ter portas toomanage / domínios de lista branca em Olá nível firewall corporativo conforme exigido por fontes de dados respectivo. Esta tabela usa apenas o Banco de Dados SQL do Azure, o SQL Data Warehouse do Azure e o Azure Data Lake Store como exemplos.   

Olá tabela a seguir fornece **porta de entrada** requisitos para Olá **firewall do windows**.

| Portas de entrada | Descrição | 
| ------------- | ----------- | 
| 8050 (TCP) | Exigido pelo Olá credential manager aplicativo toosecurely definir credenciais para repositórios de dados local no gateway de saudação. | 

![Requisitos de porta do gateway](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>Configurações de IP/lista de permissões no armazenamento de dados
Alguns repositórios de dados na nuvem Olá também exigem lista branca de endereço IP do computador Olá acessá-los. Verifique se endereço IP de saudação do computador do gateway Olá na lista branca configurado adequadamente no firewall.

Olá seguintes armazenamentos de dados de nuvem exigem lista branca do endereço IP do computador do gateway hello. Alguns desses armazenamentos de dados, por padrão, podem não exigir lista branca de endereço IP de saudação. 

- [Banco de Dados SQL do Azure](../sql-database/sql-database-firewall-configure.md) 
- [SQL Data Warehouse do Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Repositório Azure Data Lake](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Pergunta:** Olá Gateway pode ser compartilhado entre as fábricas de dados diferente?
**Resposta:** Ainda não damos suporte a esse recurso. No entanto, estamos trabalhando de forma ativa para implementá-lo.

**Pergunta:** quais são os requisitos de porta de saudação para Olá gateway toowork?
**Resposta:** Gateway faz conexões com base em HTTP tooopen internet. Olá **portas de saída 443 e 80** devem ser abertas para gateway toomake essa conexão. Abra **8050 de porta de entrada** apenas no nível de máquina hello (não no nível do firewall corporativo) para o aplicativo do Gerenciador de credenciais. Se o banco de dados do SQL Azure ou Azure SQL Data Warehouse é usado como origem / destino, você terá que tooopen **1433** porta também. Para obter mais informações, consulte a seção [Configurações de firewall e endereços IP na lista de permissões](#firewall-configurations-and-whitelisting-ip-address-of gateway). 

**Pergunta:** Quais são os requisitos de certificado do Gateway?
**Resposta:** gateway atual requer um certificado que é usado pelo aplicativo do Gerenciador de credenciais Olá para a configuração segura de credenciais do repositório de dados. Esse certificado é um certificado autoassinado criado e configurado pela instalação do gateway hello. Em vez disso, você pode usar seu próprio certificado TLS/SSL. Para obter mais informações, consulte a seção [Aplicativo gerenciador de credenciais de clique único](#click-once-credentials-manager-app). 

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre o desempenho da atividade de cópia, consulte [Guia desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md).

 
