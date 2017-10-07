---
title: "aaaAuthorization - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Estrutura de segurança: Autorização | Atenuações 
| Produto/serviço | Artigo |
| --------------- | ------- |
| **Limite de confiança de computador** | <ul><li>[Verifique se as ACLs apropriadas estão toorestrict configurado não autorizado acesso toodata no dispositivo de saudação](#acl-restricted-access)</li><li>[Garantir que os conteúdos confidenciais do usuário armazenados no aplicativo sejam armazenados no diretório do perfil do usuário](#sensitive-directory)</li><li>[Certifique-se de que os aplicativos de Olá implantado são executados com privilégios mínimos](#deployed-privileges)</li></ul> |
| **Aplicativo Web** | <ul><li>[Impor uma ordem sequencial de etapas durante o processamento dos fluxos de lógica de negócios](#sequential-logic)</li><li>[Implementar a enumeração de tooprevent do mecanismo de limitação de taxa](#rate-enumeration)</li><li>[Garantir que um sistema de autorização adequado esteja em vigor e que o princípio dos privilégios mínimos seja seguido](#principle-least-privilege)</li><li>[As decisões de autorização de acesso a recursos e a lógica de negócios não devem ser baseadas em parâmetros de solicitação de entrada](#logic-request-parameters)</li><li>[Garantir que conteúdos e recursos não sejam enumeráveis ou estejam acessíveis por meio da navegação forçada](#enumerable-browsing)</li></ul> |
| **Banco de dados** | <ul><li>[Certifique-se de que contas com menos privilégios são usadas tooconnect tooDatabase server](#privileged-server)</li><li>[Implementar locatários de tooprevent de segurança de nível de linha de acessar dados de outras pessoas](#rls-tenants)</li><li>[A função sysadmin deve ter apenas usuários necessários válidos](#sysadmin-users)</li></ul> |
| **Gateway de Nuvem IoT** | <ul><li>[Conecte-se tooCloud Gateway usando tokens com menos privilégios](#cloud-least-privileged)</li></ul> |
| **Hub de Eventos do Azure** | <ul><li>[Usar uma chave SAS com a permissão somente envio para gerar tokens de dispositivo](#sendonly-sas)</li><li>[Não use tokens de acesso que fornecem acesso direto toohello Hub de eventos](#access-tokens-hub)</li><li>[Conecte-se tooEvent usando a SAS do Hub de chaves que tenham permissões mínimas Olá necessário](#sas-minimum-permissions)</li></ul> |
| **Azure DocumentDB** | <ul><li>[Use o recurso tokens tooconnect tooDocumentDB sempre que possível](#resource-docdb)</li></ul> |
| **Limite de Confiança do Azure** | <ul><li>[Habilitar o gerenciamento de acesso refinado tooAzure assinatura usando o RBAC](#grained-rbac)</li></ul> |
| **Limite de confiança do Service Fabric** | <ul><li>[Restringir as operações de toocluster de acesso do cliente usando o RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Executar a modelagem de segurança e usar a segurança no nível do campo onde for necessário](#modeling-field)</li></ul> |
| **Portal do Dynamics CRM** | <ul><li>[Executar a modelagem de segurança de contas portais tendo em mente que modelo de segurança Olá para portal Olá é diferente do restante de saudação do CRM](#portal-security)</li></ul> |
| **Armazenamento do Azure** | <ul><li>[Conceder permissões refinadas em um intervalo de entidades no Armazenamento de Tabelas do Azure](#permission-entities)</li><li>[Habilitar a conta de armazenamento tooAzure de controle de acesso baseado em função (RBAC) usando o Gerenciador de recursos do Azure](#rbac-azure-manager)</li></ul> |
| **Cliente móvel** | <ul><li>[Implementar detecção de modificação ou desbloqueio implícito](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Referência de classe fraca no WCF](#weak-class-wcf)</li><li>[Controle de autorização implementado no WCF](#wcf-authz)</li></ul> |
| **API da Web** | <ul><li>[Implementar mecanismos de autorização apropriados na API Web ASP.NET](#authz-aspnet)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Executar verificações de autorização no dispositivo Olá se ele dá suporte a várias ações que requerem diferentes níveis de permissão](#device-permission)</li></ul> |
| **Gateway de Campo de IoT** | <ul><li>[Executar verificações de autorização no campo Gateway de saudação se ele dá suporte a várias ações que requerem diferentes níveis de permissão](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Verifique se as ACLs apropriadas estão toorestrict configurado não autorizado acesso toodata no dispositivo de saudação

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Verifique se as ACLs apropriadas estão toorestrict configurado não autorizado acesso toodata no dispositivo de saudação|

## <a id="sensitive-directory"></a>Garantir que os conteúdos confidenciais do usuário armazenados no aplicativo sejam armazenados no diretório do perfil do usuário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Garanta que os conteúdos confidenciais do usuário armazenados no aplicativo sejam armazenados no diretório do perfil do usuário. Isso é tooprevent vários usuários de saudação do computador de acessar dados de outras.|

## <a id="deployed-privileges"></a>Certifique-se de que os aplicativos de Olá implantado são executados com privilégios mínimos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que o aplicativo hello implantado é executado com menos privilégios. |

## <a id="sequential-logic"></a>Impor uma ordem sequencial de etapas durante o processamento dos fluxos de lógica de negócios

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Em ordem tooverify neste estágio foi executado por meio de por um usuário original, você deseja tooenforce Olá aplicativo tooonly negócios lógica fluxos de processo na ordem de etapas sequenciais, com todas as etapas sendo processadas no tempo humano realistas e não processa fora de ordem, ignorado etapas, processados etapas de outro usuário ou muito rapidamente enviada transações.|

## <a id="rate-enumeration"></a>Implementar a enumeração de tooprevent do mecanismo de limitação de taxa

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Verifique se os identificadores confidenciais são aleatórios. Implemente o controle CAPTCHA em páginas anônimas. Assegure que erros e exceções não revelem dados específicos.|

## <a id="principle-least-privilege"></a>Garantir que um sistema de autorização adequado esteja em vigor e que o princípio dos privilégios mínimos seja seguido

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>princípio Olá significa fornecendo uma conta de usuário os privilégios mínimos que são essenciais toothat trabalho dos usuários. Por exemplo, um usuário de backup não precisa de software tooinstall: assim, usuário de backup Olá tem direitos toorun somente aplicativos e de backup relacionados a backup. Quaisquer outros privilégios, como instalar um novo software, serão bloqueados. Olá princípio se aplica também usuário de computador pessoal tooa que geralmente funciona em uma conta de usuário normal e abre uma conta com privilégios, protegido por senha (ou seja, um superusuário) somente quando situação Olá absolutamente necessárias. </p><p>Esse princípio também pode ser aplicadas tooyour aplicativos web. Em vez de apenas dependendo de métodos de autenticação baseada em função usando sessões, em vez disso, queremos tooassign privilégios toousers por meio de um sistema de autenticação com base em banco de dados. Ainda usamos sessões em ordem tooidentify se Olá usuário estava conectado corretamente, apenas agora, em vez de atribuir a esse usuário com uma função específica, atribuí-lo com privilégios tooverify quais ações que ele privilegiadas tooperform no sistema de saudação. Também uma grande pro desse método é, sempre que um usuário tem toobe atribuído menos privilégios, que suas alterações serão aplicadas imediatamente hello como Olá atribuindo não dependem de sessão Olá que tinha tooexpire primeiro.</p>|

## <a id="logic-request-parameters"></a>As decisões de autorização de acesso a recursos e a lógica de negócios não devem ser baseadas em parâmetros de solicitação de entrada

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Sempre que você está verificando se um usuário é restrito tooreview determinados dados, acesso Olá restrições devem ser processados no servidor. Olá userID deve ser armazenado dentro de uma variável de sessão no logon e deve ser usado tooretrieve dados de usuário do banco de dados de saudação |

### <a name="example"></a>Exemplo
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Agora um invasor possíveis não pode violar e alterar a operação do aplicativo hello desde que o identificador para recuperar Olá dados hello tratado no lado do servidor.

## <a id="enumerable-browsing"></a>Garantir que conteúdos e recursos não sejam enumeráveis ou estejam acessíveis por meio da navegação forçada

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Confidenciais estático e arquivos de configuração não devem ser mantidos em Olá web raiz. Para conteúdo toobe necessária não público, acesso adequado deve ser aplicados ou remoção de saudação conteúdo em si.</p><p>Além disso, navegação forçada é geralmente combinado com informações de toogather de técnicas de força bruta tentando tooaccess tantos URLs como tooenumerate possíveis diretórios e arquivos em um servidor. Os invasores podem procurar todas as variações dos arquivos mais comuns existentes. Por exemplo, uma pesquisa de arquivo de senha incluiria os arquivos psswd.txt, password.htm, password.dat e outras variações.</p><p>toomitigate isso, recursos de detecção de força bruta tentativas deve ser incluída.</p>|

## <a id="privileged-server"></a>Certifique-se de que contas com menos privilégios são usadas tooconnect tooDatabase server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Hierarquia de permissões de banco de dados SQL](https://msdn.microsoft.com/library/ms191465), [Protegíveis de banco de dados SQL](https://msdn.microsoft.com/library/ms190401) |
| **Etapas** | Contas com menos privilégios devem ser usado tooconnect toohello. Logon do aplicativo deve ser restrito no banco de dados de saudação e só deve executar procedimentos armazenados selecionados. e não deve conceder acesso direto à tabela. |

## <a id="rls-tenants"></a>Implementar locatários de tooprevent de segurança de nível de linha de acessar dados de outras pessoas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure, OnPrem |
| **Atributos**              | Versão do SQL - V12, Versão do SQL - MsSQL2016 |
| **Referências**              | [Segurança em Nível de Linha (RLS) do SQL Server](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Etapas** | <p>Segurança em nível de linha permite que os clientes toocontrol acesso toorows em uma tabela de banco de dados com base em características de saudação do usuário Olá executando uma consulta (por exemplo, grupo associação ou contexto de execução).</p><p>Segurança de nível de linha (RLS) simplifica o design de saudação e codificação de segurança em seu aplicativo. O RLS permite tooimplement restrições no acesso de linha de dados. Por exemplo, garantindo que os funcionários podem acessar somente as linhas de dados que são pertinentes tootheir departamento ou restringir um dados acesso tooonly Olá dados tootheir relevantes da empresa do cliente.</p><p>lógica de restrição de acesso de saudação é localizado na camada de banco de dados de saudação em vez de longe dos dados de saudação em outra camada de aplicativo. sistema de banco de dados de saudação aplica restrições de acesso de saudação toda vez que acesso a dados é tentado em qualquer nível. Isso torna o sistema de segurança hello mais robusto e confiável, reduzindo a área da superfície Olá Olá do sistema de segurança.</p><p>|

Observe que a RLS como um recurso de banco de dados de caixa é tooSQL aplicável somente a partir de 2016 do servidor e banco de dados do SQL Azure. Se o recurso RLS de fora da caixa de saudação não está implementado, deve ser garante que o acesso a dados é restrito usando exibições e procedimentos

## <a id="sysadmin-users"></a>A função sysadmin deve ter apenas usuários necessários válidos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Hierarquia de permissões de banco de dados SQL](https://msdn.microsoft.com/library/ms191465), [Protegíveis de banco de dados SQL](https://msdn.microsoft.com/library/ms190401) |
| **Etapas** | Membros da função de servidor fixa SysAdmin do hello devem ser muito limitada e nunca contêm contas usadas por aplicativos.  Examine lista de saudação de usuários na função hello e remover qualquer conta desnecessária|

## <a id="cloud-least-privileged"></a>Conecte-se tooCloud Gateway usando tokens com menos privilégios

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Opção de gateway - Hub IoT do Azure |
| **Referências**              | [Controle de acesso do Hub IoT](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Etapas** | Fornece privilégios mínimos componentes de toovarious de permissões que se conectam tooCloud Gateway (IoT Hub). Um exemplo típico: o componente de gerenciamento/provisionamento de dispositivos usa os recursos de leitura/gravação do Registro, e o processador de eventos (ASA) usa o recurso de conexão de serviço. Dispositivos individuais se conectam usando as credenciais do dispositivo.|

## <a id="sendonly-sas"></a>Usar uma chave SAS com a permissão somente envio para gerar tokens de dispositivo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Hub de Eventos do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral do modelo de autenticação e segurança dos Hubs de Eventos](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Etapas** | Uma chave SAS é usado toogenerate tokens de dispositivo individual. Usar uma chave SAS permissões apenas para enviar ao gerar token do dispositivo Olá para um determinado publicador|

## <a id="access-tokens-hub"></a>Não use tokens de acesso que fornecem acesso direto toohello Hub de eventos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Hub de Eventos do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral do modelo de autenticação e segurança dos Hubs de Eventos](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Etapas** | Um token que concede hub de eventos de toohello acesso direto não deve ser fornecido o dispositivo toohello. Usando um token com menos privilégios para dispositivo Olá que fornece acesso somente tooa publicador deve ajudar a identificar e lista negra-se encontrado toobe um invasor ou dispositivo esteja comprometida.|

## <a id="sas-minimum-permissions"></a>Conecte-se tooEvent usando a SAS do Hub de chaves que tenham permissões mínimas Olá necessário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Hub de Eventos do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral do modelo de autenticação e segurança dos Hubs de Eventos](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Etapas** | Fornece privilégios mínimos a aplicativos de back-end de toovarious de permissões que se conectam toohello Hub de eventos. Gerar chaves SAS separadas para cada aplicativo de back-end e fornecem apenas as permissões necessárias de saudação - toothem Send, Receive ou gerenciar.|

## <a id="resource-docdb"></a>Use o recurso tokens tooconnect tooCosmos banco de dados sempre que possível

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Azure Document DB | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Um token de recursos é associado um recurso de permissão de documentos e capturas Olá a relação entre o usuário de saudação de uma permissão de banco de dados e hello que o usuário tem para um recurso de aplicativo do DocumentDB específico (por exemplo, a coleção, o documento). Sempre use uma saudação tooaccess token de recurso DocumentDB se o cliente Olá não pode ser confiável com manipulação de chaves mestres ou somente leitura - como um aplicativo de usuário final como um cliente móvel ou área de trabalho. Use a chave mestra ou chaves somente leitura de aplicativos back-end que podem armazenar essas chaves com segurança.|

## <a id="grained-rbac"></a>Habilitar o gerenciamento de acesso refinado tooAzure assinatura usando o RBAC

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Etapas** | O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure. Usando o RBAC, você pode conceder somente a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos.|

## <a id="cluster-rbac"></a>Restringir as operações de toocluster de acesso do cliente usando o RBAC

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure |
| **Referências**              | [Controle de acesso baseado em função para clientes do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Etapas** | <p>Malha do serviço do Azure oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário. Controle de acesso permite Olá administrador toolimit acesso toocertain cluster as operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura.</p><p>Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.</p><p>Você pode especificar funções de cliente Olá dois (cliente e administrador) em tempo de saudação da criação do cluster fornecendo certificados separados para cada.</p>|

## <a id="modeling-field"></a>Executar a modelagem de segurança e usar a segurança no nível do campo onde for necessário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Execute a modelagem de segurança e use a segurança no nível do campo onde for necessário.|

## <a id="portal-security"></a>Executar a modelagem de segurança de contas portais tendo em mente que modelo de segurança Olá para portal Olá é diferente do restante de saudação do CRM

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Portal do Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Executar a modelagem de segurança de contas portais tendo em mente que modelo de segurança Olá para portal Olá é diferente do restante de saudação do CRM|

## <a id="permission-entities"></a>Conceder permissões refinadas em um intervalo de entidades no Armazenamento de Tabelas do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de armazenamento - Tabela |
| **Referências**              | [Como toodelegate acessar tooobjects em sua conta de armazenamento do Azure usando a SAS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Etapas** | Em determinados cenários de negócios, o armazenamento de tabela do Azure pode ser necessário toostore dados confidenciais que permite que partes toodifferent. Por exemplo, dados confidenciais pertencem toodifferent países. Nesses casos, assinaturas SAS podem ser construídas especificando Olá partição e a linha de intervalos de chaves, que um usuário pode acessar determinado país de tooa específico de dados.| 

## <a id="rbac-azure-manager"></a>Habilitar a conta de armazenamento tooAzure de controle de acesso baseado em função (RBAC) usando o Gerenciador de recursos do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Como toosecure sua conta de armazenamento com controle de acesso baseado em função (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Etapas** | <p>Ao criar uma nova conta de armazenamento, você seleciona o modelo de implantação Clássico ou o do Azure Resource Manager. modelo clássico de saudação de criação de recursos no Azure permite apenas a assinatura de toohello acesso tudo ou nada e hello, por sua vez, a conta de armazenamento.</p><p>Com o modelo do Azure Resource Manager Olá, coloque o conta de armazenamento Olá em um recurso grupo e controle de acesso toohello plano de gerenciamento de conta de armazenamento específico usando o Azure Active Directory. Por exemplo, você pode conceder a usuários específicos Olá capacidade tooaccess Olá chaves conta de armazenamento, enquanto outros usuários podem exibir informações sobre a conta de armazenamento hello, mas não é possível acessar chaves de conta de armazenamento hello.</p>|

## <a id="rooting-detection"></a>Implementar detecção de modificação ou desbloqueio implícito

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvel | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Os aplicativos devem proteger seus próprios dados de configuração e usuários no caso de o telefone ser modificado ou desbloqueado. A modificação ou o desbloqueio consistem em um acesso não autorizado, que os usuários normalmente não fazem em seus próprios telefones. Portanto o aplicativo deve ter a lógica de detecção implícita na inicialização do aplicativo, toodetect se phone Olá tem raiz.</p><p>a lógica de detecção Olá pode simplesmente acessando arquivos qual usuário raiz normalmente somente pode acessar, por exemplo:</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Se o aplicativo hello pode acessar qualquer um desses arquivos, ele indicará que o aplicativo hello está sendo executado como usuário raiz.</p>|

## <a id="weak-class-wcf"></a>Referência de classe fraca no WCF

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | <p>sistema de saudação usa uma referência de classe fraca, que pode permitir que um invasor código tooexecute não autorizado. Olá programa faz referência a uma classe definida pelo usuário que não é identificada exclusivamente. Quando o .NET carregar esta classe levemente identificado, Olá CLR tipo carregador procura classe Olá Olá seguintes locais no hello especificado ordem:</p><ol><li>Se o assembly de saudação do tipo hello for conhecido, pesquisas de carregador Olá Olá de redirecionamento locais, GAC, Olá assembly atual do arquivo de configuração usando informações de configuração e Olá diretório base do aplicativo</li><li>Se o assembly hello for desconhecido, pesquisas de carregador Olá Olá assembly atual, mscorlib e localização de saudação retornada pelo manipulador de eventos TypeResolve Olá</li><li>Essa ordem de pesquisa do CLR pode ser modificada com ganchos como Olá encaminhamento de tipo de mecanismo e o evento de AppDomain.TypeResolve de saudação</li></ol><p>Se um invasor explorar a ordem de pesquisa CLR Olá criando uma classe alternativa Olá mesmo nome e colocá-lo em um local alternativo que Olá CLR será carregado pela primeira vez, Olá CLR acidentalmente execute Olá fornecido pelo invasor código</p>|

### <a name="example"></a>Exemplo
Olá `<behaviorExtensions/>` WCF tooadd uma extensão específica WCF comportamento personalizado classe tooa instrui o elemento do arquivo de configuração WCF Olá abaixo.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
Usar nomes totalmente qualificados (fortes) identifica exclusivamente um tipo e aumenta ainda mais a segurança do sistema. Use nomes de assembly totalmente qualificado ao registrar tipos em arquivos Machine. config e App. config de saudação.

### <a name="example"></a>Exemplo
Olá `<behaviorExtensions/>` elemento Olá WCF do arquivo de configuração abaixo instrui WCF tooadd comportamento personalizado referenciadas fortemente classe tooa WCF extensão específica.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>Controle de autorização implementado no WCF

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | <p>Esse serviço não usa um controle de autorização. Quando um cliente chamar um serviço WCF em particular, o WCF fornece vários esquemas de autorização que verificam o que chamador Olá tem método de serviço permissão tooexecute hello no servidor de saudação. Se os controles de autorização não estiverem habilitados para os serviços do WCF, um usuário autenticado pode ter seus privilégios elevados.</p>|

### <a name="example"></a>Exemplo
Olá seguinte configuração instrui o nível de autorização WCF toonot seleção saudação do cliente Olá ao executar o serviço de saudação:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Use um tooverify de esquema de autorização de serviço que Olá chamador do método de serviço hello é autorizado toodo assim. O WCF fornece dois modos e permite a definição de saudação de um esquema de autorização personalizada. modo de UseWindowsGroups Olá usa usuários e funções do Windows e modo de UseAspNetRoles Olá usa um provedor de função do ASP.NET, como o SQL Server, tooauthenticate.

### <a name="example"></a>Exemplo
Olá configuração a seguir instrui o WCF toomake-se de que o cliente Olá é parte do grupo de administradores de saudação antes de executar o serviço de adicionar Olá:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
serviço Hello, em seguida, é declarado da seguinte hello:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Implementar mecanismos de autorização apropriados na API Web ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, MVC5 |
| **Atributos**              | N/D, Provedor de Identidade - ADFS, Provedor de Identidade - Azure AD |
| **Referências**              | [Autenticação e autorização na API Web ASP.NET](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Etapas** | <p>Informações de função para os usuários do aplicativo hello podem ser derivadas do AD do Azure ou declarações do ADFS se o aplicativo hello depende deles como provedor de identidade ou aplicativo hello em si pode fornecido. Em qualquer um desses casos, implementação de autorização personalizada Olá deve validar informações de função de usuário de saudação.</p><p>Informações de função para os usuários do aplicativo hello podem ser derivadas do AD do Azure ou declarações do ADFS se o aplicativo hello depende deles como provedor de identidade ou aplicativo hello em si pode fornecido. Em qualquer um desses casos, implementação de autorização personalizada Olá deve validar informações de função de usuário de saudação.</p>

### <a name="example"></a>Exemplo
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Todos os controladores de hello e métodos de ação que deve tooprotected devem ser decorados com acima do atributo.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Executar verificações de autorização no dispositivo Olá se ele dá suporte a várias ações que requerem diferentes níveis de permissão

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Olá dispositivo deve autorizar Olá chamador toocheck se Olá visitante tiver uma ação de Olá Olá necessárias permissões tooperform solicitada. Para permite, por exemplo, digamos que Olá dispositivo é um Smart Lock de porta pode ser monitorado na nuvem de saudação plus fornece funcionalidades como bloquear remotamente porta hello.</p><p>Olá Smart Lock porta fornece a funcionalidade de desbloqueio somente quando alguém fisicamente vem próximo porta Olá com um cartão. Nesse caso, hello implementação do comando remoto hello e controle deve ser feita de forma que ele não fornece qualquer porta da funcionalidade toounlock hello como gateway de nuvem de saudação não é autorizado toosend uma porta de saudação do comando toounlock.</p>|

## <a id="field-permission"></a>Executar verificações de autorização no campo Gateway de saudação se ele dá suporte a várias ações que requerem diferentes níveis de permissão

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Olá campo Gateway deve autorizar Olá chamador toocheck se Olá visitante tiver uma ação de Olá Olá necessárias permissões tooperform solicitada. Para que, por exemplo, deve haver permissões diferentes para um usuário administrador de interface de API tooconfigure um campo gateway v/s dispositivos usados que se conectam tooit.|
