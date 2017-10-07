---
title: "Notas de versão do catálogo de dados aaaAzure | Microsoft Docs"
description: "Notas de versão do Catálogo de Dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Notas de versão do Catálogo de Dados do Azure
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Notas de versão de 20 de novembro de 2015 saudação do catálogo de dados do Azure
### <a name="opening-data-sources-in-power-bi-desktop"></a>Abrindo fontes no Power BI Desktop
Ao usar a opção de hello "Abrir no Power BI Desktop" hello **Data Catalog do Azure** portal, os usuários podem encontrar um dos dois problemas em Olá aplicativo Power BI Desktop:

* É exibida uma caixa de diálogo com o título hello "Não é possível tooOpen documento"
* Olá aplicativo Power BI Desktop é aberto, mas arquivo hello aparece toobe vazio

Para cada situação, o problema de Olá pode ser resolvido ao baixar e instalar a versão mais recente de saudação do Power BI Desktop de [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Notas de versão de 13 de novembro de 2015 saudação do catálogo de dados do Azure
### <a name="registering-and-connecting-tooteradata"></a>Registrar e conectar-se tooTeradata
Ao se conectar a fontes de dados de tooTeradata usuários devem ter instalado o driver ODBC Teradata correto de saudação que corresponde ao bitness da saudação (32 bits ou 64 bits) do software hello está sendo usado.

A partir dessa ADC data de lançamento, Olá mais recente [driver ODBC Teradata para windows (versão 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) é compatível com o Office 2013, mas não com o Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Notas de versão de 13 de julho de 2015 saudação do catálogo de dados do Azure
### <a name="registering-and-connecting-toooracle-database"></a>Registrar e conectar-se tooOracle banco de dados
Quando se conectar tooOracle usuários de fontes de dados de banco de dados deve ter instalado drivers Oracle corretos Olá que corresponde ao bitness da saudação (32 bits ou 64 bits) do software hello está sendo usado.

* Ao registrar fontes de dados Oracle em um computador executando o Windows de 32 bits, drivers de Oracle de 32 bits Olá serão usados.
* Ao registrar fontes de dados Oracle em um computador executando o Windows de 64 bits, drivers de Oracle de 64 bits Olá serão usados.
* Ao se conectar a fontes de dados tooOracle usando o Excel em um computador executando a versão de 32 bits de saudação do Microsoft Office, inclusive no Windows de 64 bits, drivers de Oracle de 32 bits Olá serão usados
* Ao se conectar a fontes de dados tooOracle usando o Excel em um computador executando a versão de 64 bits de saudação do Microsoft Office, drivers de Oracle de 64 bits Olá serão usados.

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Registrar e conectar-se tooSQL Server Reporting Services
Suporte para fontes de dados do SQL Server Reporting Services (SSRS) é atualmente limitada tooNative modo somente os servidores. O suporte para o SSRS no modo SharePoint será adicionado em uma versão posterior.

### <a name="opening-data-assets-in-excel"></a>Abrindo ativos de dados no Excel
Ao abrir ativos de dados no Microsoft Excel de saudação **Data Catalog do Azure** portal, os usuários podem ser solicitados com uma **aviso de segurança do Microsoft Excel** caixa de diálogo. Este é o padrão, comportamento esperado e os usuários podem selecionar **habilitar** toocontinue.

Para obter mais informações, veja [Habilitar ou desabilitar alertas de segurança sobre links e arquivos de sites suspeitos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Registro da fonte de dados e configuração de proxy e política
Os usuários podem encontrar uma situação em que eles podem fazer logon no portal do toohello Data Catalog do Azure, mas quando tentarem toolog na ferramenta de registro de origem toohello dados encontram uma mensagem de erro que impede o registro em log.

Há duas causas possíveis para esse comportamento de problema:

**Causa 1: Configuração de serviços de Federação do Active Directory** ferramenta de registro de fonte de dados Olá usa autenticação de formulários toovalidate logons de usuário no Active Directory. Para um logon bem-sucedido, autenticação de formulários deve ser habilitada na política de autenticação Global de saudação pelo administrador do Active Directory.

Em algumas situações, esse comportamento de erro pode ocorrer somente quando o usuário Olá é na rede da empresa de hello, ou somente quando o usuário hello está se conectando fora Olá rede da empresa. Olá política de autenticação Global permite toobe de métodos de autenticação habilitado separadamente para conexões de intranet e extranet. Erros de logon poderão ocorrer se a autenticação de formulários não está habilitada para rede de saudação do qual Olá usuário está se conectando.

Para obter mais informações, consulte [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).

**Causa 2: Configuração de proxy de rede** se a rede corporativa Olá usa um servidor proxy, ferramenta de registro de saudação pode não ser capaz de tooconnect tooAzure do Active Directory por meio do proxy de saudação. Os usuários podem garantir essa ferramenta de registro de saudação editando o arquivo de configuração da ferramenta Olá, adicionar este arquivo de toohello seção:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


arquivo de RegistrationTool.exe.config de saudação toolocate, inicie a ferramenta de registro de saudação e, em seguida, abra o utilitário do Gerenciador de tarefas do Windows hello. Na guia de detalhes de saudação no Gerenciador de tarefas, clique duas vezes em RegistrationTool.exe e escolha Abrir local do arquivo no menu pop-up de saudação.
