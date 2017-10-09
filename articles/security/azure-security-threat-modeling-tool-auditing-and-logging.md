---
title: "aaaAuditing e registro em log - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Quadro de segurança: Auditoria e log | Atenuações 
| Produto/Serviço | Artigo |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identificar entidades sensíveis em sua solução e implementar a auditoria de alteração](#sensitive-entities)</li></ul> |
| **Aplicativo Web** | <ul><li>[Certifique-se de que a auditoria e registro em log é aplicado em aplicativo hello](#auditing)</li><li>[Certifique-se de que a rotação de log e separação estão em vigor](#log-rotation)</li><li>[Certifique-se de que o aplicativo hello não registra dados confidenciais do usuário](#log-sensitive-data)</li><li>[Verifique se os arquivos de Log e auditoria tem acesso restrito](#log-restricted-access)</li><li>[Certifique-se de que os eventos de gerenciamento de usuário estão registrados](#user-management)</li><li>[Verifique se o sistema de saudação tem embutidas defesas contra uso indevido](#inbuilt-defenses)</li><li>[Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](#diagnostics-logging)</li></ul> |
| **Banco de dados** | <ul><li>[Verifique se a auditoria de logon é habilitada no SQL Server](#identify-sensitive-entities)</li><li>[Ativar a detecção de ameaças no SQL Azure](#threat-detection)</li></ul> |
| **Armazenamento do Azure** | <ul><li>[Use o Azure Storage Analytics tooaudit acesso do armazenamento do Azure](#analytics)</li></ul> |
| **WCF** | <ul><li>[Implementar o log suficiente](#sufficient-logging)</li><li>[Implementar o tratamento de falha de auditoria suficiente](#audit-failure-handling)</li></ul> |
| **API da Web** | <ul><li>[Certifique-se de que a auditoria e registro em log é imposto no API da Web](#logging-web-api)</li></ul> |
| **Gateway de Campo de IoT** | <ul><li>[Certifique-se de que a auditoria e log apropriado é imposta no campo Gateway](#logging-field-gateway)</li></ul> |
| **Gateway de Nuvem IoT** | <ul><li>[Certifique-se de que a auditoria e log apropriado é imposta no Gateway de nuvem](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Identificar entidades sensíveis em sua solução e implementar a auditoria de alteração

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | Identificar as entidades em sua solução que contém dados confidenciais e implementar a auditoria de alteração nessas entidades e campos |

## <a id="auditing"></a>Certifique-se de que a auditoria e registro em log é aplicado em aplicativo hello

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | Habilite a auditoria e log em todos os componentes. Os logs de auditoria devem capturar o contexto do usuário. Identifique todos os eventos importantes e registre em log esses eventos. Implementar o log centralizado |

## <a id="log-rotation"></a>Certifique-se de que a rotação de log e separação estão em vigor

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | <p>Rotação de log é um processo automatizado usado na administração do sistema no qual os arquivos de log datado são arquivados. Servidores que executam aplicativos grandes geralmente registrar cada solicitação: face de saudação de registros volumosos, rotação do log é uma saudação toolimit de maneira tamanho total dos logs de saudação enquanto ainda permite que a análise dos eventos recentes. </p><p>Separação de log significa basicamente que você tenha toostore seus arquivos de log em uma partição diferente em que seu sistema operacional/aplicativo é executado na ordem tooavert uma negação de serviço de ataque ou Olá fazer downgrade do seu aplicativo, o desempenho</p>|

## <a id="log-sensitive-data"></a>Certifique-se de que o aplicativo hello não registra dados confidenciais do usuário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | <p>Verifique que você não faça quaisquer dados confidenciais que um usuário envia tooyour site. Verifique se há registro intencional, bem como os efeitos colaterais causados por problemas de design. Exemplos de dados confidenciais:</p><ul><li>Credenciais do Usuário</li><li>Número do seguro social ou outras informações de identificação</li><li>Números de cartão de crédito ou outras informações financeiras</li><li>Informações de integridade</li><li>Informações criptografadas de chaves privadas ou outros dados que podem ser usado toodecrypt</li><li>Informações do sistema ou aplicativo que podem ser usadas toomore ataques efetivamente o aplicativo hello</li></ul>|

## <a id="log-restricted-access"></a>Verifique se os arquivos de Log e auditoria tem acesso restrito

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | <p>Verifique tooensure arquivos de toolog de direitos de acesso são definidos corretamente. Contas de aplicativo devem ter acesso somente gravação e operadores e equipe de suporte deve ter acesso somente leitura, conforme necessário.</p><p>Contas de administradores são Olá somente as contas que devem ter acesso completo. Verifique a que ACL do Windows no log arquivos tooensure são restritos corretamente:</p><ul><li>Contas de aplicativos devem ter acesso somente gravação</li><li>Operadores e a equipe de suporte deve ter acesso somente leitura, conforme necessário</li><li>Os administradores são Olá somente as contas que devem ter acesso completo</li></ul>|

## <a id="user-management"></a>Certifique-se de que os eventos de gerenciamento de usuário estão registrados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | <p>Certifique-se de que o aplicativo hello monitora os eventos de gerenciamento de usuário, como logons de usuário bem-sucedidas e com falha, redefinições de senha, alterações de senha, o bloqueio de conta, o registro de usuário. Isso ajuda a toodetect e reage toopotentially qualquer comportamento suspeito. Ele também permite que dados de operações toogather; Por exemplo, tootrack quem está acessando o aplicativo hello</p>|

## <a id="inbuilt-defenses"></a>Verifique se o sistema de saudação tem embutidas defesas contra uso indevido

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas**                   | <p>Controles devem estar em vigor que lançam a exceção de segurança em caso de uso incorreto do aplicativo. Por exemplo, se a validação de entrada está em vigor e um invasor tenta tooinject código mal-intencionado que não corresponde à saudação regex, uma exceção de segurança pode ser gerada que pode ser um indicativos de uso indevido do sistema</p><p>Por exemplo, é recomendável toohave exceções de segurança registradas e as ações tomadas para Olá problemas a seguir:</p><ul><li>Validação da entrada</li><li>Violações de CSRF</li><li>Força bruta (limite superior para o número de solicitações por usuário por recurso)</li><li>Violações de carregamento de arquivo</li><ul>|

## <a id="diagnostics-logging"></a>Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de ambiente - Azure |
| **Referências**              | N/D  |
| **Etapas** | <p>Azure fornece tooassist diagnóstico interno ao depurar um aplicativo de serviço de aplicativo web. Ela também se aplica tooAPI aplicativos e aplicativos móveis. Aplicativos do serviço de aplicativo web fornecem funcionalidade de diagnóstico para obter informações de registro em log do servidor de web hello e o aplicativo da web hello.</p><p>Estes estão logicamente separados em diagnóstico de servidor Web e diagnóstico de aplicativos</p>|

## <a id="identify-sensitive-entities"></a>Verifique se a auditoria de logon é habilitada no SQL Server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Configurar a auditoria de logon](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Etapas** | <p>Auditoria de logon do servidor de banco de dados deve ser ataques de adivinhação de senha toodetect/confirmar habilitado. É importante de tentativas de logon com falha toocapture. Capturar as duas tentativas de logon bem-sucedidas e malsucedidas fornece o benefício adicional durante investigações jurídicas</p>|

## <a id="threat-detection"></a>Ativar a detecção de ameaças no SQL Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure |
| **Atributos**              | Versão do SQL - V12 |
| **Referências**              | [Introdução à Detecção de Ameaças do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Etapas** |<p>Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança. Ele fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais.</p><p>Os usuários podem explorar eventos suspeitos hello, usando a auditoria banco de dados do Azure SQL toodetermine se eles são provenientes de uma tentativa tooaccess, violação ou explorar dados no banco de dados de saudação.</p><p>A detecção de ameaças torna simples tooaddress potenciais ameaças toohello banco de dados sem a necessidade de saudação toobe um especialista em segurança ou gerenciar sistemas de monitoramento de segurança avançada</p>|

## <a id="analytics"></a>Use o Azure Storage Analytics tooaudit acesso do armazenamento do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D |
| **Referências**              | [Usando o tipo de análise de armazenamento de autorização toomonitor](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Etapas** | <p>Para cada conta de armazenamento, um pode habilitar o log de tooperform de análise de armazenamento do Azure e armazenar dados de métricas. Olá logs de análise de armazenamento fornecem informações importantes, como o método de autenticação usado por uma pessoa, ao acessar o armazenamento.</p><p>Isso pode ser muito útil se você está estreitamente preservando toostorage de acesso. Por exemplo, no armazenamento de Blob, você pode definir todos Olá contêineres tooprivate e implementar o uso de saudação de um serviço SAS ao longo de seus aplicativos. Em seguida, você pode verificar Olá regularmente logs toosee se seus blobs acessados usando chaves de conta de armazenamento hello, que podem indicar uma violação de segurança, ou se blobs Olá são públicos, mas eles não devem ser.</p>|

## <a id="sufficient-logging"></a>Implementar o log suficiente

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | <p>falta de saudação de uma trilha de auditoria adequada após um incidente de segurança pode atrapalhar os esforços forenses. Windows Communication Foundation (WCF) oferece a capacidade de saudação toolog tentativas de autenticação de êxito e/ou com falha.</p><p>Registro em log as tentativas de autenticação com falha pode avisar os administradores de possíveis ataques de força bruta. Da mesma forma, o log de eventos de autenticação bem-sucedida pode fornecer uma trilha de auditoria útil quando uma conta legítima seja comprometida. Habilitar o recurso de auditoria de segurança de serviço do WCF |

### <a name="example"></a>Exemplo
a seguir Olá é um exemplo de configuração com a auditoria ativada
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Implementar o tratamento de falha de auditoria suficiente

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | <p>Solução desenvolvida está configurada não toogenerate uma exceção quando ela falha de log de auditoria de tooan toowrite. Se WCF está configurado não toothrow uma exceção quando ele é o log de auditoria de tooan toowrite não é possível, programa hello não será notificado da falha de saudação e auditoria de eventos de segurança crítica não pode ocorrer.</p>|

### <a name="example"></a>Exemplo
Olá `<behavior/>` instrui o elemento do arquivo de configuração WCF Olá abaixo WCF toonot notificar o aplicativo hello quando WCF falha de log de auditoria de tooan toowrite.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Configure o programa de saudação do WCF toonotify sempre que o log de auditoria de tooan toowrite não é possível. programa de saudação deve ter um esquema de notificação alternativo na organização de saudação tooalert local que as trilhas de auditoria não são mantidas. 

## <a id="logging-web-api"></a>Certifique-se de que a auditoria e registro em log é imposto no API da Web

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Habilite a auditoria e log em APIs da Web. Os logs de auditoria devem capturar o contexto do usuário. Identifique todos os eventos importantes e registre em log esses eventos. Implementar o log centralizado |

## <a id="logging-field-gateway"></a>Certifique-se de que a auditoria e log apropriado é imposta no campo Gateway

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Quando vários dispositivos se conectam tooa campo Gateway, certifique-se de que as tentativas de conexão e o status de autenticação (sucesso ou falha) para dispositivos individuais são registradas e mantidas nos Olá Gateway de campo.</p><p>Além disso, em casos onde o Gateway de campo é manter Olá IoT Hub credenciais para dispositivos individuais, certifique-se de que a auditoria é executada quando essas credenciais são recuperadas. Desenvolva um processo tooperiodically carregamento Olá logs tooAzure IoT Hub/armazenamento para retenção de longo prazo.</p> |

## <a id="logging-cloud-gateway"></a>Certifique-se de que a auditoria e log apropriado é imposta no Gateway de nuvem

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Monitoramento de operações do Hub de tooIoT de Introdução](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Etapas** | <p>Design para coletar e armazenar dados de auditoria coletados por meio do monitoramento de operações de Hub IoT. Habilite Olá monitoramentos categorias a seguir:</p><ul><li>Operações de identidade do dispositivo</li><li>Comunicações do dispositivo para a nuvem</li><li>Comunicações da nuvem para o dispositivo</li><li>Conexões</li><li>Carregamentos de arquivos</li></ul>|
