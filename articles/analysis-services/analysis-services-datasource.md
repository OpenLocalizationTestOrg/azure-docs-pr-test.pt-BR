---
title: fontes de aaaData com suporte no Azure Analysis Services | Microsoft Docs
description: Descreve as fontes de fonte de dados com suporte para modelos de dados no Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Fontes de dados com suporte no Azure Analysis Services
Servidores de Analysis Services do Azure oferecem suporte a conectar fontes de toodata em nuvem hello e no local em sua organização. Todo o tempo de saudação estão sendo adicionados a fontes de dados com suporte adicional. Verifique com frequência. 

Olá, fontes de dados a seguir é atualmente suportado:

| Nuvem  |
|---|
| Armazenamento de Blobs do Azure*  |
| Banco de Dados SQL do Azure  |
| Data Warehouse do Azure |


| Configuração local  |   |   |   |
|---|---|---|---|
| Banco de Dados do Access  | Pasta* | Banco de dados Oracle  | Banco de dados Teradata |
| Active Directory*  | Documento JSON*  | Banco de Dados SQL Postgre*  |Tabela XML* |
| Serviços de análise  | Linhas de binário*  | SAP HANA*  |
| Analytics Platform System  | Banco de Dados MySQL  | SAP Business Warehouse*  | |
| Dynamics CRM*  | Feed OData*  | SharePoint*  |
| Pasta de trabalho do Excel  | Consulta ODBC  | Banco de Dados SQL  |
| Exchange*  | OLE DB  | Banco de dados Sybase  |

\*Somente modelos Tabular 1400. 

> [!IMPORTANT]
> Conectando requerem fontes de dados local tooon um [gateway de dados no local](analysis-services-gateway.md) instalado em um computador em seu ambiente.

## <a name="data-providers"></a>Provedores de dados

Modelos de dados no Azure Analysis Services podem exigir diferentes provedores de dados ao se conectar a fontes de dados toocertain. Em alguns casos, os modelos de tabela se conectar a fontes de toodata usando provedores nativo, como o SQL Server Native Client (SQLNCLI11) podem retornar um erro.

Modelos de dados que se conectam a dados na nuvem tooa origem como o banco de dados do SQL Azure, se você usar provedores nativos diferente SQLOLEDB, você verá a mensagem de erro: **"provedor de saudação 'SQLNCLI11.1' não está registrado."** Ou, se você tiver um DirectQuery modelo conectar fontes de dados local tooon, se você usar provedores nativos você verá a mensagem de erro: **"Erro ao criar o conjunto de linhas do OLE DB. Sintaxe incorreta próxima a 'LIMIT' "**.

Olá provedores de fonte de dados a seguir têm suporte para modelos de dados de DirectQuery ou na memória quando toodata conectar fontes no hello nuvem ou no local:

### <a name="cloud"></a>Nuvem
| **Fonte de dados** | **Na memória** | **DirectQuery** |
|  --- | --- | --- |
| SQL Data Warehouse do Azure |Provedor de Dados .NET Framework para SQL Server |Provedor de Dados .NET Framework para SQL Server |
| Banco de Dados SQL do Azure |Provedor de Dados .NET Framework para SQL Server |Provedor de Dados .NET Framework para SQL Server | |

### <a name="on-premises-via-gateway"></a>Local (via Gateway)
|**Fonte de dados** | **Na memória** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |Provedor de Dados .NET Framework para SQL Server |
| SQL Server |Provedor Microsoft OLE DB para SQL Server |Provedor de Dados .NET Framework para SQL Server | |
| SQL Server |Provedor de Dados .NET Framework para SQL Server |Provedor de Dados .NET Framework para SQL Server | |
| Oracle |Provedor Microsoft OLE DB para Oracle |Provedor de Dados Oracle para .NET | |
| Oracle |Provedor de Dados Oracle para .NET |Provedor de Dados Oracle para .NET | |
| Teradata |Provedor OLE DB para Teradata |Provedor de Dados Teradata para .NET | |
| Teradata |Provedor de Dados Teradata para .NET |Provedor de Dados Teradata para .NET | |
| Analytics Platform System |Provedor de Dados .NET Framework para SQL Server |Provedor de Dados .NET Framework para SQL Server | |

> [!NOTE]
> Certifique-se de que os provedores de 64 bits estejam instalados ao usar o gateway Local.
> 
> 

Ao migrar um tooAzure de modelo de tabela do SQL Server Analysis Services local do Analysis Services, talvez seja necessário toochange provedor de saudação.

**toospecify um provedor de fonte de dados**

1. No SSDT > **Gerenciador de Modelo de Tabela** > **Fontes de Dados**, clique com o botão direito em uma conexão de fonte de dados e, em seguida, clique em **Editar Fonte de Dados**.
2. Em **Editar Conexão**, clique em **avançado** tooopen janela de propriedades de adiantamento de saudação.
3. Em **definir propriedades avançadas** > **provedores**, em seguida, selecione Olá provedor apropriado.

## <a name="impersonation"></a>Representação
Em alguns casos, pode ser necessário toospecify uma representação diferente da conta. A conta de representação pode ser especificada no SSDT ou o no SSMS.

Para fontes de dados locais:

* Se estiver usando a autenticação SQL, a representação deverá ser a Conta de serviço.
* Se estiver usando a autenticação do Windows, defina o usuário/senha do Windows. Para o SQL Server, há suporte para a autenticação do Windows com uma conta de representação específica apenas para modelos de dados na memória.

Para fontes de dados de nuvem:

* Se estiver usando a autenticação SQL, a representação deverá ser a Conta de serviço.

## <a name="next-steps"></a>Próximas etapas
Se você tiver fontes de dados locais, ser se Olá de tooinstall [gateway local](analysis-services-gateway.md).   
toolearn mais sobre como gerenciar seu servidor no SSDT ou o SSMS, consulte [gerenciar seu servidor](analysis-services-manage.md).

