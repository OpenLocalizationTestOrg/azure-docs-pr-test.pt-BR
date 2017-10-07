---
title: "aaaAuthentication - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Estrutura de segurança: autenticação | Atenuações 
| Produto/Serviço | Artigo |
| --------------- | ------- |
| **Aplicativo Web**    | <ul><li>[Considere o uso de um tooWeb de tooauthenticate do mecanismo de autenticação padrão aplicativo](#standard-authn-web-app)</li><li>[Os aplicativos devem lidar com cenários de autenticação com falha com segurança](#handle-failed-authn)</li><li>[Habilitar upgrade ou autenticação adaptável](#step-up-adaptive-authn)</li><li>[Verifique se as interfaces administrativas estão adequadamente bloqueadas](#admin-interface-lockdown)</li><li>[Implemente funcionalidades de senha esquecida com segurança](#forgot-pword-fxn)</li><li>[Verifique se as políticas de conta e senha são implementadas](#pword-account-policy)</li><li>[Implementar controles tooprevent username enumeração](#controls-username-enum)</li></ul> |
| **Banco de dados** | <ul><li>[Quando possível, use a autenticação do Windows para conectar-se tooSQL Server](#win-authn-sql)</li><li>[Quando possível, use autenticação do Active Directory do Azure para conectar-se tooSQL banco de dados](#aad-authn-sql)</li><li>[Quando o modo de autenticação do SQL for usado, verifique se as políticas de conta e senha são impostas no SQL server](#authn-account-pword)</li><li>[Não use a Autenticação do SQL em bancos de dados independentes](#autn-contained-db)</li></ul> |
| **Hub de Eventos do Azure** | <ul><li>[Use credenciais de autenticação por dispositivo usando tokens SaS](#authn-sas-tokens)</li></ul> |
| **Limite de Confiança do Azure** | <ul><li>[Habilitar Autenticação Multifator do Azure para administradores do Azure](#multi-factor-azure-admin)</li></ul> |
| **Limite de confiança do Service Fabric** | <ul><li>[Restringir o acesso anônimo tooService Cluster de malha](#anon-access-cluster)</li><li>[Verifique se o certificado de cliente para o nó de Service Fabric serviço é diferente do certificado de nó para nó](#fabric-cn-nn)</li><li>[Use clusters de malha do AAD tooauthenticate clientes tooservice](#aad-client-fabric)</li><li>[Verifique se os certificados de service fabric são obtidos de uma CA (autoridade de certificação) aprovada](#fabric-cert-ca)</li></ul> |
| **Identity Server** | <ul><li>[Use cenários de autenticação padrão com suporte no Servidor de Identidade](#standard-authn-id)</li><li>[Substituir saudação padrão Identity Server cache de token por uma alternativa escalonável](#override-token)</li></ul> |
| **Limite de confiança de computador** | <ul><li>[Verifique se os binários do aplicativo implantado são assinados digitalmente](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[Habilitar a autenticação ao conectar-se tooMSMQ filas no WCF](#msmq-queues)</li><li>[WCF-não não definir mensagem clientCredentialType toonone](#message-none)</li><li>[WCF-não não definido transporte clientCredentialType toonone](#transport-none)</li></ul> |
| **API da Web** | <ul><li>[Certifique-se de técnicas de autenticação padrão são usado toosecure APIs da Web](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Use cenários de autenticação padrão com suporte no Azure Active Directory](#authn-aad)</li><li>[Substituir saudação padrão ADAL cache de token por uma alternativa escalonável](#adal-scalable)</li><li>[Certifique-se de que o TokenReplayCache é tooprevent usado reprodução de saudação de tokens de autenticação de ADAL](#tokenreplaycache-adal)</li><li>[Use o token de bibliotecas ADAL toomanage solicitações de OAuth2 tooAAD de clientes (ou AD local)](#adal-oauth2)</li></ul> |
| **Gateway de Campo de IoT** | <ul><li>[Autenticar dispositivos conectados toohello Gateway de campo](#authn-devices-field)</li></ul> |
| **Gateway de Nuvem IoT** | <ul><li>[Certifique-se de que os dispositivos conectados tooCloud gateway são autenticados](#authn-devices-cloud)</li><li>[Usar credenciais de autenticação por dispositivo](#authn-cred)</li></ul> |
| **Armazenamento do Azure** | <ul><li>[Certifique-se de que somente Olá necessário contêineres e blobs recebem acesso de leitura anônimo](#req-containers-anon)</li><li>[Conceder acesso limitado tooobjects no armazenamento do Azure usando SAS ou SAP](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Considere o uso de um tooWeb de tooauthenticate do mecanismo de autenticação padrão aplicativo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | <p>A autenticação é o processo de saudação em que uma entidade comprova sua identidade, normalmente por meio de credenciais, como um nome de usuário e senha. Há vários protocolos de autenticação disponíveis que podem ser considerados. Alguns deles são listados abaixo:</p><ul><li>Certificados do cliente</li><li>Baseado no Windows</li><li>Baseado em formulários</li><li>Federação - ADFS</li><li>Federação – Azure AD</li><li>Federação - Servidor de Identidade</li></ul><p>Considere o uso de um processo de origem do Olá de tooidentify do mecanismo de autenticação padrão</p>|

## <a id="handle-failed-authn"></a>Os aplicativos devem lidar com segurança com os cenários de autenticação com falha

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | <p>Aplicativos que explicitamente autenticar usuários devem lidar com cenários de autenticação com falha deve securely.hello mecanismo de autenticação:</p><ul><li>Negar acesso tooprivileged recursos quando a autenticação falhar</li><li>Exibir uma mensagem de erro genérica após falha na autenticação e acesso negado</li></ul><p>Teste de:</p><ul><li>Proteção de recursos privilegiados após logons com falha</li><li>Será exibida uma mensagem de erro genérica em evento(s) de autenticação com falha e acesso negado</li><li>As contas são desabilitadas após um número excessivo de tentativas com falha</li><ul>|

## <a id="step-up-adaptive-authn"></a>Habilitar upgrade ou autenticação adaptável

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | <p>Verifique se o aplicativo hello tem autorização adicional (como migrar ou autenticação adaptável, através da autenticação multifator como o envio de OTP no SMS, email etc. ou pedir reautenticação) para o usuário Olá enfrenta antes de obterem acesso informações de toosensitive. Esta regra também se aplica para tornar a conta de tooan alterações importantes ou ação</p><p>Isso também significa que adaptação Olá de autenticação tem toobe implementado de tal maneira que o aplicativo hello impõe corretamente autorização contextual assim como toonot permitir manipulação não autorizada por meio no exemplo, violação de parâmetro</p>|

## <a id="admin-interface-lockdown"></a>Verifique se as interfaces administrativas estão adequadamente bloqueadas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | Olá primeira solução é toogrant acesso somente a partir de um determinado origem IP intervalo toohello interface administrativa. Se essa solução não seria possível que ele é sempre recomendável tooenforce uma autenticação Step-up ou adaptável para fazer logon na interface administrativa Olá |

## <a id="forgot-pword-fxn"></a>Implemente funcionalidades de senha esquecida com segurança

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | <p>Olá é primeiro tooverify que esqueceu a senha e outros caminhos de recuperação enviam um link, incluindo uma senha de token, em vez da saudação de ativação de tempo limite em si. Autenticação adicional com base em tokens de software (por exemplo, SMS token móveis aplicativos nativos, etc.) pode ser necessária bem antes de link de saudação é enviado pela. Em segundo lugar, você não deve bloquear as contas de usuários Olá durante o processo de saudação de obtenção de uma nova senha está em andamento.</p><p>Isso poderia gerar tooa negação de ataque de serviço sempre que um invasor decide bloqueio toointentionally usuários Olá com um ataque automatizado. Em terceiro lugar, sempre que a nova solicitação de senha Olá foi definida em andamento, mensagem de saudação que é exibir deve ser generalizada na enumeração de nome de usuário de tooprevent de ordem. Quarto, sempre impedir Olá uso de senhas antigas e implemente uma política de senha forte.</p> |

## <a id="pword-account-policy"></a>Verifique se as políticas de conta e senha são implementadas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Detalhes | <p>A política de conta e senha em conformidade com a política organizacional e as práticas recomendadas deve ser implementadas.</p><p>toodefend contra a força bruta e de dicionário com base em adivinhação: política de senha forte deve ser implementado tooensure aos usuários criarem uma senha complexa (por exemplo, comprimento mínimo de 12 caracteres, caracteres especiais e alfanuméricos).</p><p>Políticas de bloqueio de conta podem ser implementadas em Olá maneira a seguir:</p><ul><li>**Limite de bloqueio flexível:** essa pode ser uma boa opção para proteger os usuários contra ataques de força bruta. Por exemplo, sempre que o usuário Olá insere uma senha incorreta aplicativo hello de três vezes pode bloquear conta Olá por um minuto em ordem tooslow processo Olá de aplicar a sua senha, tornando-o menos lucrativo para Olá invasor tooproceed de força bruta. Se você tooimplement rígido contramedidas de limite de bloqueio para este exemplo, você deve obter um "Dos" bloqueando permanentemente as contas. Como alternativa, o aplicativo pode gerar uma OTP (senha) e enviá-lo fora de banda (por email, sms etc.) toohello usuário. Outra abordagem possível tooimplement CAPTCHA depois que um número limite de tentativas for atingido.</li><li>**Limite de bloqueio rígido:** esse tipo de bloqueio deve ser aplicado sempre que você detecta um usuário atacar o seu aplicativo e contador-lo por meio de bloquear sua conta permanentemente até que uma equipe de resposta teve tempo toodo sua análise forense. Após esse processo, você pode decidir toogive Olá ao usuário sua conta ou tomar ações legais adicionais em relação a ele. Esse tipo de abordagem impede que o invasor Olá penetrem ainda mais sua infraestrutura e aplicativo.</li></ul><p>toodefend contra ataques em padrão e contas previsíveis, verifique se todas as chaves e senhas são substituíveis e são geradas ou substituídas após a instalação.</p><p>Se o aplicativo hello tem tooauto-gerar senhas, verifique se senhas Olá gerado são aleatórias e tem alta entropia.</p>|

## <a id="controls-username-enum"></a>Implementar controles tooprevent username enumeração

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Todas as mensagens de erro devem ser generalizadas na enumeração de nome de usuário de tooprevent de ordem. Além disso, às vezes você não pode evitar o vazamento de recursos, como uma página de registro de informações. Aqui você precisa de métodos de limitação de taxa de toouse como CAPTCHA tooprevent um ataque automatizado por um invasor. |

## <a id="win-authn-sql"></a>Quando possível, use a autenticação do Windows para conectar-se tooSQL Server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | OnPrem |
| **Atributos**              | Versão do SQL - Todas |
| **Referências**              | [SQL Server - escolher um modo de autenticação](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Etapas** | Autenticação do Windows usa o protocolo de segurança Kerberos, fornece imposição de política de senha com a validação de toocomplexity de relação para senhas fortes, fornece suporte para bloqueio de conta e dá suporte à expiração de senha.|

## <a id="aad-authn-sql"></a>Quando possível, use autenticação do Active Directory do Azure para conectar-se tooSQL banco de dados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure |
| **Atributos**              | Versão do SQL - V12 |
| **Referências**              | [Conectando tooSQL banco de dados, usando o Azure Active Directory Authentication](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Etapas** | **Versão mínima:** V12 de banco de dados do SQL Azure necessário toouse autenticação do AAD do Azure SQL Database tooallow contra Olá Directory do Microsoft |

## <a id="authn-account-pword"></a>Quando o modo de autenticação do SQL for usado, verifique se as políticas de conta e senha são impostas no SQL server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Política de senha do SQL Server](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Etapas** | Ao usar a Autenticação do SQL Server, são criados logons no SQL Server que não se baseiam em contas de usuário do Windows. Nome de usuário hello e senha Olá são criadas usando o SQL Server e armazenados no SQL Server. O SQL Server pode usar mecanismos de política de senha do Windows. Ele pode aplicar Olá mesmas políticas de complexidade e validade usadas no Windows toopasswords usado dentro do SQL Server. |

## <a id="autn-contained-db"></a>Não use a Autenticação do SQL em bancos de dados independentes

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | OnPrem, SQL Azure |
| **Atributos**              | Versão do SQL - MSSQL2012, Versão do SQL - V12 |
| **Referências**              | [Práticas recomendadas de segurança com bancos de dados contidos](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Etapas** | ausência de saudação de uma política de senha aplicada pode aumentar a probabilidade de saudação de uma credencial fraca que está sendo estabelecida em um banco de dados independente. Aproveite a Autenticação do Windows. |

## <a id="authn-sas-tokens"></a>Use credenciais de autenticação por dispositivo usando tokens SaS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Hub de Eventos do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral do modelo de autenticação e segurança dos Hubs de Eventos](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Etapas** | <p>modelo de segurança de Hubs de eventos Olá baseia-se em uma combinação de tokens de assinatura de acesso compartilhado (SAS) e editores de eventos. nome do publicador Olá representa Olá DeviceID que recebe o token de saudação. Isso ajuda a associar tokens Olá gerados com dispositivos respectivos hello.</p><p>Todas as mensagens são marcadas com o originador no lado do serviço, o que permite a detecção de tentativas de falsificação de origem na carga. Na autenticação de dispositivos, gerar um por publicador exclusivo do dispositivo SaS token tooa no escopo.</p>|

## <a id="multi-factor-azure-admin"></a>Habilitar Autenticação Multifator do Azure para administradores do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [O que é a Autenticação Multifator do Azure?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Etapas** | <p>A autenticação multifator (MFA) é um método de autenticação que requer mais de um método de verificação e adiciona uma segunda camada crítica de segurança toouser entradas e transações. Ela funciona exigindo dois ou mais Olá métodos de verificação a seguir:</p><ul><li>Algo que você sabe (normalmente, uma senha)</li><li>Algo que você tem (um dispositivo confiável que não pode ser facilmente clonado, como um telefone)</li><li>Algo seu (biometria)</li><ul>|

## <a id="anon-access-cluster"></a>Restringir o acesso anônimo tooService Cluster de malha

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure  |
| **Referências**              | [Cenários de segurança do cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Etapas** | <p>Clusters sempre devem ser protegido tooprevent não autorizado usuários conectem cluster tooyour, especialmente quando ele tiver cargas de trabalho de produção em execução.</p><p>Ao criar um cluster do service fabric, certifique-se de que o modo de segurança hello está definido muito "seguro" e configure o certificado de servidor x. 509 Olá necessário. Criar um cluster "inseguro" permitirá que qualquer tooit tooconnect de usuário anônimo se toohello de pontos de extremidade de gerenciamento, ele expõe Internet pública.</p>|

## <a id="fabric-cn-nn"></a>Verifique se o certificado de cliente para o nó de Service Fabric serviço é diferente do certificado de nó para nó

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure, ambiente - autônomo |
| **Referências**              | [Segurança de certificado de cliente para o nó do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [conectar tooa cluster seguro usando o certificado de cliente](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Etapas** | <p>Segurança de certificado de cliente para o nó é configurada durante a criação de cluster Olá por meio de saudação portal do Azure, modelos do Gerenciador de recursos ou um modelo JSON autônomo, especificando um certificado de cliente de administração e/ou um certificado de cliente do usuário.</p><p>Olá administrador usuário cliente certificados de cliente e que você especificar devem ser diferentes de certificados primários e secundários Olá especificado para segurança de nó para nó.</p>|

## <a id="aad-client-fabric"></a>Use clusters de malha do AAD tooauthenticate clientes tooservice

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure |
| **Referências**              | [Cenários de segurança - recomendações de segurança de cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Etapas** | Clusters em execução no Azure também podem proteger acesso a pontos de extremidade de gerenciamento toohello usando o Azure Active Directory (AAD), além de certificados de cliente. Para clusters do Azure, é recomendável que você use o AAD segurança tooauthenticate clientes e certificados para segurança de nó para nó.|

## <a id="fabric-cert-ca"></a>Verifique se os certificados de service fabric são obtidos de uma CA (autoridade de certificação) aprovada

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure |
| **Referências**              | [Certificados X.509 e Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Etapas** | <p>O Service Fabric usa certificados de servidor X.509 para autenticar clientes e nós.</p><p>Tooconsider algumas coisas importantes durante o uso de certificados em malhas de serviço:</p><ul><li>Os certificados usados em clusters que executam cargas de trabalho de produção devem ser criados por meio de um serviço de certificado do Windows Server configurado corretamente ou obtidos por meio de uma AC (Autoridade de Certificação) aprovada. Olá autoridade de certificação pode ser uma CA externa aprovada ou uma adequadamente gerenciado interno chave pública infra-estrutura (PKI)</li><li>Nunca use nenhum certificado temporário ou de teste em produção criado com ferramentas como MakeCert.exe</li><li>Você pode usar um certificado autoassinado, mas deve fazer isso somente para clusters de teste e não em produção</li></ul>|

## <a id="standard-authn-id"></a>Use cenários de autenticação padrão com suporte no Servidor de Identidade

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [IdentityServer3 - Olá visão geral](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Etapas** | <p>Abaixo está Olá típicas interações com suporte pelo servidor de identidade:</p><ul><li>Os navegadores se comunicam com aplicativos Web</li><li>Os aplicativos Web se comunicam com APIs Web (às vezes, por conta própria e, às vezes, em nome do usuário)</li><li>Aplicativos baseados em navegador se comunicam com APIs Web</li><li>Aplicativos nativos se comunicam com APIs Web</li><li>Aplicativos baseados em servidor se comunicam com APIs Web</li><li>As APIs Web se comunicam com as APIs Web (às vezes, por conta própria e, às vezes, em nome do usuário)</li></ul>|

## <a id="override-token"></a>Substituir saudação padrão Identity Server cache de token por uma alternativa escalonável

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Implantação de Servidor de Identidade - cache](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Etapas** | <p>IdentityServer tem um cache na memória interno simples. Enquanto isso é bom para aplicativos nativos de pequena escala, ele não é dimensionado para aplicativos de camada e de back-end mid para Olá motivos a seguir:</p><ul><li>Esses aplicativos são acessados por vários usuários simultaneamente. Salvar todos os tokens de acesso no hello mesmo repositório cria problemas de isolamento e apresenta desafios ao operar em grande escala: muitos usuários, cada um com tantas tokens como recursos Olá Olá acessos de aplicativo em seu nome, pode significar grandes números e pesquisa muito cara operações</li><li>Normalmente, esses aplicativos são implantados em topologias distribuídas, em que vários nós devem ter acesso toohello mesmo cache</li><li>Os tokens em cache devem sobreviver a desativações e reciclagem de processo</li><li>Para todos os Olá acima motivos, durante a implementação de aplicativos da web, é recomendável o cache de token do servidor de identidade padrão Olá toooverride uma alternativa dimensionável como o cache Redis do Azure</li></ul>|

## <a id="binaries-signed"></a>Verifique se os binários do aplicativo implantado são assinados digitalmente

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que os binários do aplicativo implantado são assinados digitalmente para que possa ser verificada integridade Olá dos binários de saudação|

## <a id="msmq-queues"></a>Habilitar a autenticação ao conectar-se tooMSMQ filas no WCF

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Etapas** | Programa falhar na autenticação de tooenable ao conectar-se tooMSMQ filas, um invasor pode enviar anonimamente a fila de toohello mensagens para processamento. Se a autenticação não for usado tooconnect tooan MSMQ fila usada toodeliver um programa de tooanother de mensagem, um invasor pode enviar uma mensagem anônima é mal-intencionado.|

### <a name="example"></a>Exemplo
Olá `<netMsmqBinding/>` elemento Olá WCF do arquivo de configuração abaixo instrui a autenticação do WCF toodisable ao conectar-se a fila do MSMQ tooan para entrega de mensagens.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Configure a autenticação de domínio do Windows ou o certificado de toorequire MSMQ em todos os momentos para as mensagens de entrada ou saídas.

### <a name="example"></a>Exemplo
Olá `<netMsmqBinding/>` elemento Olá WCF do arquivo de configuração abaixo instrui a autenticação de certificado do WCF tooenable ao conectar-se a fila do MSMQ tooan. cliente de saudação é autenticado usando certificados x. 509. certificado de cliente Olá deve estar presente no repositório de certificados de saudação do servidor de saudação.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>WCF-não não definir mensagem clientCredentialType toonone

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | Tipo de Credencial de Cliente - Nenhuma |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortalecer](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | ausência de saudação de autenticação significa todos é capaz de tooaccess esse serviço. Um serviço que não autentica seus clientes permite acesso a usuários tooall. Configure Olá tooauthenticate de aplicativo em relação às credenciais de cliente. Isso pode ser feito definindo Olá mensagem clientCredentialType tooWindows ou certificado. |

### <a name="example"></a>Exemplo
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>WCF-não não definido transporte clientCredentialType toonone

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, .NET Framework 3 |
| **Atributos**              | Tipo de Credencial de Cliente - Nenhuma |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortalecer](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | ausência de saudação de autenticação significa todos é capaz de tooaccess esse serviço. Um serviço que não autentica seus clientes permite tooaccess de todos os usuários de sua funcionalidade. Configure Olá tooauthenticate de aplicativo em relação às credenciais de cliente. Isso pode ser feito definindo Olá transporte clientCredentialType tooWindows ou certificado. |

### <a name="example"></a>Exemplo
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Certifique-se de técnicas de autenticação padrão são usado toosecure APIs da Web

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Autenticação e Autorização na API Web ASP.NET](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), [Serviços de Autenticação Externa com a API Web do ASP.NET (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **Etapas** | <p>A autenticação é o processo de saudação em que uma entidade comprova sua identidade, normalmente por meio de credenciais, como um nome de usuário e senha. Há vários protocolos de autenticação disponíveis que podem ser considerados. Alguns deles são listados abaixo:</p><ul><li>Certificados do cliente</li><li>Baseado no Windows</li><li>Baseado em formulários</li><li>Federação - ADFS</li><li>Federação – Azure AD</li><li>Federação - Servidor de Identidade</li></ul><p>Links na seção de referências de saudação fornecem detalhes de baixo nível sobre como cada um dos esquemas de autenticação Olá pode ser implementado toosecure uma API da Web.</p>|

## <a id="authn-aad"></a>Use cenários de autenticação padrão com suporte no Azure Active Directory

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | AD do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Cenários de Autenticação do Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Exemplos de Código do Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Guia do Desenvolvedor do Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Etapas** | <p>O Azure AD (Azure Active Directory) simplifica a autenticação para os desenvolvedores fornecendo identidade como um serviço, com suporte para protocolos padrão do setor, como OAuth 2.0 e OpenID Connect. Abaixo está Olá cinco cenários de aplicativos principais com suporte pelo AD do Azure:</p><ul><li>Navegador tooWeb aplicativo de Web: um usuário precisa toosign no aplicativo web tooa que é protegido pelo AD do Azure</li><li>Aplicativo de página única (SPA): Um usuário precisa toosign no aplicativo de página única tooa que é protegido pelo AD do Azure</li><li>TooWeb do aplicativo nativo API: um aplicativo nativo que é executado em um telefone, tablet ou PC necessidades tooauthenticate tooget um usuário recursos de uma API da web que é protegido pelo AD do Azure</li><li>Web Application tooWeb API: um aplicativo web precisa tooget recursos de uma API da web protegida pelo AD do Azure</li><li>TooWeb daemon ou aplicativo de servidor API: um aplicativo daemon ou um aplicativo de servidor sem interface de usuário da web precisa tooget recursos de uma API da web protegida pelo AD do Azure</li></ul><p>Consulte para obter detalhes de implementação de baixo nível toohello links na seção de referências de saudação</p>|

## <a id="adal-scalable"></a>Substituir saudação padrão ADAL cache de token por uma alternativa escalonável

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | AD do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Autenticação Moderna com o Azure Active Directory para Aplicativos Web](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/), [Usando o Redis como cache de token ADAL](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)  |
| **Etapas** | <p>cache de padrão de saudação usa ADAL (biblioteca de autenticação do Active Directory) é um cache na memória que se baseia em um armazenamento estático, todo o processo disponível. Enquanto isso funciona para aplicativos nativos, ele não é dimensionado para aplicativos de camada e de back-end mid para Olá motivos a seguir:</p><ul><li>Esses aplicativos são acessados por vários usuários simultaneamente. Salvar todos os tokens de acesso no hello mesmo repositório cria problemas de isolamento e apresenta desafios ao operar em grande escala: muitos usuários, cada um com tantas tokens como recursos Olá Olá acessos de aplicativo em seu nome, pode significar grandes números e pesquisa muito cara operações</li><li>Normalmente, esses aplicativos são implantados em topologias distribuídas, em que vários nós devem ter acesso toohello mesmo cache</li><li>Os tokens em cache devem sobreviver a desativações e reciclagem de processo</li></ul><p>Para todos os Olá acima motivos, durante a implementação de aplicativos da web, é recomendável toooverride saudação padrão ADAL cache de token por uma alternativa dimensionável como o cache Redis do Azure.</p>|

## <a id="tokenreplaycache-adal"></a>Certifique-se de que o TokenReplayCache é tooprevent usado reprodução de saudação de tokens de autenticação de ADAL

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | AD do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Autenticação Moderna com o Azure Active Directory para Aplicativos Web](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) |
| **Etapas** | <p>propriedade de TokenReplayCache Olá permite que os desenvolvedores toodefine um cache de reprodução de token, um repositório que pode ser usado para não salvar os tokens para finalidade de saudação de verificar se nenhum token pode ser usado mais de uma vez.</p><p>Esta é uma medida em relação a um ataque comum, hello adequadamente chamado ataques de reprodução de token: um invasor interceptando token Olá enviada na entrada tente toosend-toohello aplicativo novamente ("Repetir"-lo) para estabelecer uma nova sessão. Por exemplo, no OIDC-concessão de código de fluxo, após a autenticação bem-sucedida do usuário, uma solicitação muito "/ signin oidc" ponto de extremidade da terceira parte confiável Olá é feito com "id_token", "código" e "estado" parâmetros.</p><p>saudação de terceira parte confiável valida a solicitação e estabelece uma nova sessão. Se um adversário captura essa solicitação e repete, ele pode estabelecer uma sessão bem-sucedida e o usuário de saudação falso. presença de saudação de nonce Olá no OpenID Connect pode limitar mas não totalmente eliminar circunstâncias Olá no qual ataque Olá pode ser aplicada com êxito. tooprotect seus aplicativos, os desenvolvedores podem fornecer uma implementação de ITokenReplayCache e atribuir um tooTokenReplayCache de instância.</p>|

### <a name="example"></a>Exemplo
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Exemplo
Aqui está um exemplo da implementação da interface de ITokenReplayCache hello. (Personalize e implemente sua estrutura de cache específica do projeto)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
cache de saudação implementada tem toobe referenciado nas opções de OIDC via hello "TokenValidationParameters" propriedade da seguinte maneira.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Observe que eficácia de saudação tootest dessa configuração, fazer logon no seu aplicativo local protegido OIDC e capturar a solicitação de saudação muito`"/signin-oidc"` ponto de extremidade no fiddler. Quando a proteção de saudação não está em vigor, a repetição dessa solicitação no fiddler definirá um novo cookie de sessão. Quando a solicitação de saudação é reproduzida depois Olá o TokenReplayCache proteção é adicionada, o aplicativo hello lançará uma exceção da seguinte maneira:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Use o token de bibliotecas ADAL toomanage solicitações de OAuth2 tooAAD de clientes (ou AD local)

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | AD do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Etapas** | <p>saudação do Azure AD authentication Library (ADAL) permite que cliente aplicativo desenvolvedores tooeasily autenticar usuários toocloud ou Active Directory (AD) local e, em seguida, obter tokens de acesso para proteger chamadas de API.</p><p>A ADAL tem muitos recursos que tornam a autenticação mais fácil para os desenvolvedores, como o suporte assíncrono, um cache de token configurável que armazena os tokens de acesso e de atualização, atualização automática de token quando um token de acesso expira e um token de atualização está disponível, e muito mais.</p><p>Controlando a maioria da complexidade hello, ADAL pode ajudar o desenvolvedor se concentre na lógica de negócios em seus aplicativos e proteja facilmente os recursos sem ser um especialista em segurança. Bibliotecas separadas estão disponíveis para .NET, JavaScript (cliente e Node.js), iOS, Android e Java.</p>|

## <a id="authn-devices-field"></a>Autenticar dispositivos conectados toohello Gateway de campo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que cada dispositivo é autenticado pelo campo Gateway de saudação antes de aceitar dados a partir deles e antes de facilitando upstream comunicações com hello Gateway de nuvem. Além disso, verifique se os dispositivos se conectam com uma credencial por dispositivo, para que dispositivos individuais possam ser identificados exclusivamente.|

## <a id="authn-devices-cloud"></a>Certifique-se de que os dispositivos conectados tooCloud gateway são autenticados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, C#, Node.JS,  |
| **Atributos**              | N/A, Opção de gateway - Hub IoT do Azure |
| **Referências**              | N/A, [Hub IoT do Azure com .NET](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [Introdução ao hub IoT e Nó JS](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [Protegendo a IoT com SAS e certificados](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Repositório Git](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Etapas** | <ul><li>**Genérico:** dispositivo de saudação autenticar usando a segurança de camada de transporte (TLS) ou IPSec. A infraestrutura deve dar suporte ao uso da PSK (chave pré-compartilhada) nos dispositivos que não conseguem lidar com a criptografia assimétrica completa. Aproveite o Azure AD e o OAuth.</li><li>**C#:** ao criar uma instância de DeviceClient, por padrão, Olá criar método cria uma instância de DeviceClient que usa Olá AMQP protocolo toocommunicate com o IoT Hub. Olá toouse protocolo HTTPS, usar a substituição de saudação do método de criação de hello que permite que o protocolo de saudação toospecify. Se você usar o protocolo HTTPS de saudação, você também deve adicionar Olá `Microsoft.AspNet.WebApi.Client` saudação do NuGet pacote tooyour projeto tooinclude `System.Net.Http.Formatting` namespace.</li></ul>|

### <a name="example"></a>Exemplo
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Exemplo
**Node.JS: Autenticação**
#### <a name="symmetric-key"></a>Chave simétrica
* Criar um hub IoT no azure
* Crie uma entrada no registro de identidade de dispositivo Olá
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Criar um dispositivo simulado
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>Token SAS
* É gerado internamente ao usar a chave simétrica, mas também pode gerá-la e usá-la explicitamente
* Defina um protocolo: `var Http = require('azure-iot-device-http').Http;`
* Crie um token sas:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Conecte-se usando um token sas: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certificados
* Gerar um X509 autoassinado certificado usando uma ferramenta como toogenerate OpenSSL uma. cert na chave e uma chave arquivos toostore Olá certificado e hello respectivamente
* Provisione um dispositivo que aceite a conexão segura usando certificados.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Conectar um dispositivo usando um certificado
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Usar credenciais de autenticação por dispositivo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT  | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Opção de gateway - Hub IoT do Azure |
| **Referências**              | [Tokens de segurança do Hub IoT do Azure](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Etapas** | Use credenciais de autenticação por dispositivo usando tokens SaS com base na chave do dispositivo ou no certificado de cliente, em vez de políticas de acesso compartilhado de nível de Hub IoT. Isso evita a reutilização de saudação de tokens de autenticação de um gateway de dispositivo ou um campo por outro |

## <a id="req-containers-anon"></a>Certifique-se de que somente Olá necessário contêineres e blobs recebem acesso de leitura anônimo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | StorageType - Blob |
| **Referências**              | [Gerenciar o acesso de leitura anônimo toocontainers e blobs](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [assinaturas de acesso compartilhado, parte 1: modelo SAS Olá Noções básicas sobre](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Etapas** | <p>Por padrão, um contêiner e todos os blobs dentro dele podem ser acessados somente pelo proprietário Olá Olá da conta de armazenamento. contêiner de tooa toogive usuários anônimos permissões de leitura e seus blobs, um pode definir acesso público do hello contêiner permissões tooallow. Usuários anônimos podem ler blobs dentro de um contêiner publicamente acessível sem autenticar a solicitação de saudação.</p><p>Os contêineres fornecem Olá opções para gerenciar o acesso do contêiner a seguir:</p><ul><li>Acesso completo de leitura pública: os dados de contêiner e blob podem ser lidos por solicitação anônima. Os clientes podem enumerar blobs dentro do contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.</li><li>Acesso de leitura pública somente para blobs: os dados blob nesse contêiner podem ser lidos por solicitação anônima, mas os dados do contêiner não estão disponíveis. Os clientes não podem enumerar blobs no contêiner Olá por solicitação anônima</li><li>Acesso de leitura não público: dados de contêiner e blob podem ser lidos pelo proprietário da conta Olá somente</li></ul><p>O acesso anônimo é ideal para cenários em que determinados blobs sempre devem estar disponíveis para acesso de leitura anônimo. Para um controle refinado, é possível criar uma assinatura de acesso compartilhado, que permite o acesso de toodelegate restringido usando permissões diferentes e em um intervalo de tempo especificado. Verifique se contêineres e blobs, que podem conter dados confidenciais, não recebem acesso anônimo acidentalmente</p>|

## <a id="limited-access-sas"></a>Conceder acesso limitado tooobjects no armazenamento do Azure usando SAS ou SAP

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D |
| **Referências**              | [Assinaturas de acesso compartilhado, parte 1: Modelo SAS Noções básicas sobre Olá](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [assinaturas de acesso compartilhado, parte 2: criar e usar uma SAS com armazenamento de Blob](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [como toodelegate acessar tooobjects usando sua conta Assinaturas de acesso compartilhado e políticas de acesso armazenada](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Etapas** | <p>Usar uma assinatura de acesso compartilhado (SAS) é um tooobjects de acesso de toogrant limitado de maneira eficiente em uma conta tooother os clientes de armazenamento, sem ter a chave de acesso de conta tooexpose. Olá SAS é um URI que abrange a seus parâmetros de consulta todas as informações de saudação necessárias para autenticados para acessam o recurso de armazenamento de tooa. tooaccess recursos de armazenamento com hello SAS, Olá cliente precisa apenas de toopass no construtor apropriado do toohello Olá SAS ou método.</p><p>Você pode usar uma SAS quando desejar tooprovide acesso tooresources no seu cliente de tooa de conta de armazenamento que não pode ser confiável com a chave de conta hello. As chaves de conta de armazenamento incluem tanto uma chave primária e secundária, que concedem a conta de acesso administrativo a tooyour e todos os recursos de saudação nele. Exposição de qualquer uma de suas chaves de conta abre sua possibilidade de toohello de conta de uso mal-intencionado ou negligente. Assinaturas de acesso compartilhado fornecem uma alternativa segura que permite que outros clientes tooread, gravação e exclusão de dados em sua conta de armazenamento de acordo com as permissões do toohello que você concedeu e sem necessidade de chave de conta hello.</p><p>Se você tiver um conjunto lógico de parâmetros que são sempre semelhantes, o uso de SAP (política de acesso armazenada) será uma ideia melhor. Porque o uso de uma SAS derivada de uma política de acesso armazenado oferece Olá capacidade toorevoke que SAS imediatamente, é Olá recomendado tooalways de prática recomendada usar políticas de acesso armazenado quando possível.</p>|
