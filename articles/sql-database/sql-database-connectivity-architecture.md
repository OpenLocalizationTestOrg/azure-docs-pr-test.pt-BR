---
title: arquitetura de conectividade de banco de dados SQL do aaaAzure | Microsoft Docs
description: Este documento explica hello Azure SQLDB conectividade arquitetura de dentro do Azure ou de fora do Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Arquitetura de Conectividade do Banco de Dados SQL do Azure 

Este artigo explica a arquitetura de conectividade de banco de dados do Azure SQL hello e explica como diferentes componentes de saudação funcionam toodirect instância de tooyour de tráfego do banco de dados do SQL Azure. Esses componentes de conectividade de banco de dados do Azure SQL função toohello de tráfego de rede toodirect banco de dados do Azure com clientes se conectam de dentro do Azure e clientes se conectam de fora do Azure. Este artigo também fornece toochange de exemplos de script, como ocorre a conectividade e considerações de saudação relacionadas a configurações de conectividade do toochanging saudação padrão. Se houver alguma dúvida depois de ler este artigo, entre em contato com o Dhruv em dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Arquitetura de conectividade

Olá diagrama a seguir fornece uma visão geral de saudação arquitetura de conectividade de banco de dados SQL. 

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/architecture-overview.png)


Olá etapas a seguir descrevem como uma conexão é estabelecida tooan banco de dados de SQL do Azure através de hello Azure SQL Database software balanceador de carga (SLB) e o gateway de banco de dados SQL do hello.

- Clientes no Azure ou fora do Azure se conectar toohello SLB, que tem um endereço IP público e escuta na porta 1433.
- Olá SLB direciona o gateway de banco de dados SQL do tráfego toohello.
- gateway Olá redireciona Olá tráfego toohello proxy corretas middleware.
- Olá proxy middleware redireciona Olá tráfego toohello SQL Azure banco de dados apropriado.

> [!IMPORTANT]
> Cada um desses componentes tem distribuído negação de proteção de serviço (DDoS) interna em rede hello e camada de aplicativo hello.
>

## <a name="connectivity-from-within-azure"></a>Conectividade de dentro do Azure

Se você estiver se conectando de dentro do Azure, as conexões têm uma política de conexão de **Redirecionamento** por padrão. Uma política de **redirecionar** significa que conexões após a sessão TCP Olá estabelecida toohello banco de dados do SQL Azure, sessão de saudação do cliente é então redirecionado toohello proxy middleware com IP virtual de destino do toohello uma alteração de que de hello Azure SQL Database gateway toothat de saudação proxy middleware. Depois disso, todos os pacotes subsequentes fluam diretamente por meio do middleware de proxy hello, ignorando o gateway de banco de dados do Azure SQL hello. Olá diagrama a seguir ilustra esse fluxo de tráfego.

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Conectividade de fora do Azure

Se você estiver se conectando de fora do Azure, as conexões têm uma política de conexão de **Proxy** por padrão. Uma política de **Proxy** significa que a sessão TCP de saudação é estabelecido por meio do gateway de banco de dados do Azure SQL hello e todos os pacotes subsequentes fluam através de Olá gateway. Olá diagrama a seguir ilustra esse fluxo de tráfego.

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Endereços IP de gateway do Banco de Dados SQL do Azure

tooconnect tooan SQL Azure banco de dados de recursos locais, você precisa de tooallow rede de saída tráfego toohello banco de dados de SQL Azure gateway para sua região do Azure. As conexões vão somente por meio do gateway de saudação ao conectar-se no modo de Proxy, que é o padrão de saudação ao conectar-se de recursos locais.

Olá a tabela a seguir lista Olá IPs primários e secundários do gateway de banco de dados do Azure SQL Olá para todas as regiões de dados. Para algumas regiões, há dois endereços IP. Essas regiões, endereço IP primário Olá é Olá atual endereço IP do gateway de saudação e Olá segundo endereço IP é um endereço IP de failover. endereço de failover de saudação é Olá endereço toowhich podemos pode mover seu servidor tookeep Olá disponibilidade do serviço alta. Para essas regiões, é recomendável permitir saída tooboth endereços IP hello. endereço IP da segunda Olá pertence pela Microsoft e não escutará todos os serviços até que ele seja ativado por conexões de tooaccept do banco de dados SQL.

| Nome da Região | Endereço IP primário | Endereço IP secundário |
| --- | --- |--- |
| Leste da Austrália | 191.238.66.109 | 13.75.149.87 |
| Sudeste da Austrália | 191.239.192.109 | 13.73.109.251 |
| Sul do Brasil | 104.41.11.5 | |    
| Canadá Central | 40.85.224.249 | |    
| Leste do Canadá | 40.86.226.166 | |
| Centro dos EUA | 23.99.160.139 | 13.67.215.62 |
| Ásia Oriental | 191.234.2.139 | 52.175.33.150 |
| Leste dos EUA 1 | 191.238.6.43 | 40.121.158.30 |
| Leste dos EUA 2 | 191.239.224.107 | 40.79.84.180 |
| Centro da Índia | 104.211.96.159  | |   
| Sul da Índia | 104.211.224.146  | |
| Oeste da Índia | 104.211.160.80 | |
| Leste do Japão | 191.237.240.43 | 13.78.61.196 |
| Oeste do Japão | 191.238.68.11 | 104.214.148.156 |
| Coreia Central | 52.231.32.42 | |
| Sul da Coreia | 52.231.200.86 |  |
| Centro-Norte dos EUA | 23.98.55.75 | 23.96.178.199 |
| Norte da Europa | 191.235.193.75 | 40.113.93.91 |
| Centro-Sul dos Estados Unidos | 23.98.162.75 | 13.66.62.124 |
| Sudeste da Ásia | 23.100.117.95 | 104.43.15.0 |
| Norte do Reino Unido | 13.87.97.210 | |
| Sul do Reino Unido 1 | 51.140.184.11 | |    
| Sul do Reino Unido 2 | 13.87.34.7 | |
| Oeste do Reino Unido | 51.141.8.11  | |
| Centro-Oeste dos EUA | 13.78.145.25 | |
| Europa Ocidental | 191.237.232.75 | 40.68.37.158 |
| Oeste dos EUA 1 | 23.99.34.75 | 104.42.238.205 |
| Oeste dos EUA 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Alterar a política de conexão do Banco de Dados SQL do Azure

Olá toochange diretiva de conexão de banco de dados SQL para um servidor de banco de dados SQL, use Olá [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Se a diretiva de conexão está definida muito**Proxy**, todo o fluxo de pacotes por meio do gateway de banco de dados SQL de saudação de rede. Para essa configuração, você precisa tooallow tooonly saída hello Azure SQL Database gateway IP. Usar uma configuração de **Proxy** resulta em uma latência maior do que aquela da configuração de **Redirecionamento**. 
- Se a diretiva de conexão está definindo **redirecionar**, todos os pacotes de rede diretamente fluem toohello middleware proxy. Para essa configuração, você precisa tooallow saída toomultiple IPs. 

## <a name="script-toochange-connection-settings"></a>Configurações de conexão do script toochange

> [!IMPORTANT]
> Este script requer Olá [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

saudação de script do PowerShell a seguir mostra como toochange Olá diretiva de conexão.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Próximas etapas

- Para obter informações sobre como toochange Olá diretiva de conexão de banco de dados SQL para um servidor de banco de dados SQL, consulte [criar ou atualizar política de Conexão de servidor usando Olá REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Para obter mais informações sobre o comportamento de conexão do Banco de Dados SQL do Azure para clientes que usam ADO.NET 4.5 ou uma versão mais recente, consulte [Portas depois da 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Para obter informações sobre a visão geral do desenvolvimento de aplicativos em geral, consulte [Visão Geral do Desenvolvimento de Aplicativos do Banco de Dados SQL](sql-database-develop-overview.md).
