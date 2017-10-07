---
title: "aaaSensitive dados - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Estrutura de segurança: Dados confidenciais | Atenuações 
| Produto/serviço | Artigo |
| --------------- | ------- |
| **Limite de confiança de computador** | <ul><li>[Garantir que os binários sejam obscurecidos se contiverem informações confidenciais](#binaries-info)</li><li>[Considere usar o sistema de arquivos criptografados (EFS) é tooprotect usados os dados confidenciais específicos do usuário](#efs-user)</li><li>[Certifique-se de que os dados confidenciais armazenados pelo aplicativo hello no sistema de arquivos de saudação são criptografados](#filesystem)</li></ul> | 
| **Aplicativo Web** | <ul><li>[Certifique-se de que conteúdo confidencial não é armazenado em cache no navegador Olá](#cache-browser)</li><li>[Criptografar as seções dos arquivos de configuração do aplicativo Web que contêm dados confidenciais](#encrypt-data)</li><li>[Desabilite explicitamente o atributo HTML Olá autocomplete em formulários confidenciais e entradas](#autocomplete-input)</li><li>[Certifique-se de que os dados confidenciais exibidos na tela de saudação do usuário são mascarados](#data-mask)</li></ul> | 
| **Banco de dados** | <ul><li>[Implementar a usuários de mascaramento toolimit exposição de dados confidenciais não privilegiado de dados dinâmicos](#dynamic-users)</li><li>[Garantir que as senhas sejam armazenadas em um formato hash salgado](#salted-hash)</li><li>[Garantir que os dados confidenciais nas colunas do banco de dados sejam criptografados](#db-encrypted)</li><li>[Garantir que a criptografia no nível do banco de dados (TDE) esteja habilitada](#tde-enabled)</li><li>[Garantir que os backups de banco de dados estejam criptografados](#backup)</li></ul> | 
| **API da Web** | <ul><li>[Certifique-se de que tooWeb relevantes dados confidenciais que API não é armazenada no armazenamento do navegador](#api-browser)</li></ul> | 
| Azure Document DB | <ul><li>[Criptografar os dados confidenciais armazenados no DocumentDB](#encrypt-docdb)</li></ul> | 
| **Limite de confiança da VM da IaaS do Azure** | <ul><li>[Usar discos de tooencrypt de criptografia de disco do Azure usados por máquinas virtuais](#disk-vm)</li></ul> | 
| **Limite de confiança do Service Fabric** | <ul><li>[Criptografar segredos nos aplicativos do Service Fabric](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Executar a modelagem de segurança e usar unidades de negócios/equipes onde for necessário](#modeling-teams)</li><li>[Minimizar o recurso de tooshare de acesso em entidades críticos](#entities)</li><li>[Treinar os usuários Olá riscos associados ao recurso de compartilhamento do Dynamics CRM hello e boas práticas de segurança](#good-practices)</li><li>[Incluir uma regra de padrões de desenvolvimento que impeça a exibição dos detalhes de configuração do gerenciamento de exceções](#exception-mgmt)</li></ul> | 
| **Armazenamento do Azure** | <ul><li>[Usar o Azure Storage Service Encryption (SSE) para dados em repouso (visualização)](#sse-preview)</li><li>[Usar dados confidenciais do cliente criptografia toostore no armazenamento do Azure](#client-storage)</li></ul> | 
| **Cliente móvel** | <ul><li>[Criptografar confidenciais ou dados PII gravados armazenamento local toophones](#pii-phones)</li><li>[Ofuscar binários gerados antes de distribuir tooend usuários](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Conjunto clientCredentialType tooCertificate ou do Windows](#cert)</li><li>[O modo de segurança do WCF não está habilitado](#security)</li></ul> | 

## <a id="binaries-info"></a>Garantir que os binários sejam obscurecidos se contiverem informações confidenciais

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Garanta que os binários sejam obscurecidos se eles contiverem informações confidenciais, como segredos comerciais ou uma lógica de negócios confidenciais que não deve ser revertida. Isso é toostop inversa de engenharia de assemblies. Ferramentas como o `CryptoObfuscator` podem ser utilizadas para isso. |

## <a id="efs-user"></a>Considere usar o sistema de arquivos criptografados (EFS) é tooprotect usados os dados confidenciais específicos do usuário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Considere usar o sistema de arquivos criptografados (EFS) é usado tooprotect dados confidenciais de específicas do usuário de adversários com o computador de toohello acesso físico. |

## <a id="filesystem"></a>Certifique-se de que os dados confidenciais armazenados pelo aplicativo hello no sistema de arquivos de saudação são criptografados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que os dados confidenciais armazenados pelo aplicativo hello no sistema de arquivos de saudação são criptografados (por exemplo, usando a DPAPI), se o EFS não pode ser imposto. |

## <a id="cache-browser"></a>Certifique-se de que conteúdo confidencial não é armazenado em cache no navegador Olá

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, Formulários da Web, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Os navegadores podem armazenar informações em seus caches e históricos. Esses arquivos armazenados em cache são armazenados em uma pasta, como pasta de Temporary Internet Files Olá no caso de saudação do Internet Explorer. Quando essas páginas são chamadas novamente, o navegador de saudação exibe-los de seu cache. Se informações confidenciais são exibidos toohello usuário (como seu endereço, detalhes do cartão de crédito, número do seguro Social ou nome de usuário), essas informações podem ser armazenados no cache do navegador e, portanto, possam ser recuperados por meio de examinar o cache do navegador hello ou simplesmente pressionando o botão "Voltar" do navegador hello. Definir o valor do cabeçalho de resposta de cache-control muito "nenhum repositório" para todas as páginas. |

### <a name="example"></a>Exemplo
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Exemplo
Também é possível fazer isso usando um filtro. O exemplo abaixo pode ser usado: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Criptografar as seções dos arquivos de configuração do aplicativo Web que contêm dados confidenciais

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Como: Criptografar seções de configuração no ASP.NET 2.0 usando DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [especificando um provedor de configuração protegida](https://msdn.microsoft.com/library/68ze1hb2.aspx), [segredos de aplicativo tooprotect usando o Cofre de chaves do Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Etapas** | Arquivos de configuração como Olá Web. config, appSettings. JSON são geralmente usados toohold de informações confidenciais, incluindo nomes de usuário, senhas, cadeias de conexão de banco de dados e chaves de criptografia. Se você não proteger essas informações, o aplicativo é vulnerável tooattackers ou usuários mal-intencionados, obtenção de informações confidenciais, como nomes de conta de usuário e senhas, nomes de banco de dados e nomes de servidor. Com base no tipo de implantação da saudação (azure/local), criptografe seções confidenciais de saudação do arquivos de configuração usando a DPAPI ou serviços, como o Cofre de chaves do Azure. |

## <a id="autocomplete-input"></a>Desabilite explicitamente o atributo HTML Olá autocomplete em formulários confidenciais e entradas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN: o atributo de preenchimento automático](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [Usando o preenchimento automático com HTML](http://msdn.microsoft.com/library/ms533032.aspx), [Vulnerabilidade de limpeza de HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Preencher automaticamente de novo?](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Etapas** | atributo de preenchimento automático de saudação especifica se um formulário deve ter o recurso Preenchimento automático ativado ou desativado. Quando o recurso Preenchimento automático está ativado, Olá navegador completa automaticamente os valores com base nos valores que Olá usuário inseriu antes. Por exemplo, quando um novo nome e uma senha é inserida em um formulário e Olá formulário é enviado, navegador Olá perguntará se a senha de saudação deve ser salvo. Assim, quando o formulário Olá é exibido, Olá nome e senha são preenchidos automaticamente ou são concluídas conforme Olá nome foi digitado. Um invasor com acesso local foi possível obter a senha de texto não criptografado de saudação do cache do navegador de saudação. Por padrão, o preenchimento automático está habilitado e deve ser desabilitado explicitamente. |

### <a name="example"></a>Exemplo
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Certifique-se de que os dados confidenciais exibidos na tela de saudação do usuário são mascarados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Dados confidenciais, como senhas, números de cartão de crédito, etc. de SSN devem ser mascarados quando exibido na tela hello. Essa é a equipe de tooprevent não autorizado acessem dados hello (por exemplo, navegação shoulder senhas, exibindo números de SSN de usuários à equipe de suporte). Garanta que esses elementos de dados não estejam visíveis em texto sem formatação e sejam mascarados adequadamente. Isso tem toobe resolvido ao aceitá-los como entrada (por exemplo. tipo de entrada = "senha"), bem como exibir novamente na tela hello (por exemplo, exibir apenas Olá últimos 4 dígitos do número de cartão de crédito Olá). |

## <a id="dynamic-users"></a>Implementar a usuários de mascaramento toolimit exposição de dados confidenciais não privilegiado de dados dinâmicos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure, OnPrem |
| **Atributos**              | Versão do SQL - V12, Versão do SQL - MsSQL2016 |
| **Referências**              | [Mascaramento de dados dinâmicos](https://msdn.microsoft.com/library/mt130841) |
| **Etapas** | finalidade de saudação do mascaramento de dados dinâmicos é toolimit exposição de dados confidenciais, impedindo que os usuários que não devem ter acesso toohello dados de exibi-lo. Mascaramento de dados dinâmicos não visar tooprevent usuários de banco de dados do banco de dados toohello conectando-se diretamente e executem consultas abrangentes que exponham dados confidenciais hello. Mascaramento de dados dinâmicos é complementar tooother recursos de segurança do SQL Server (auditoria, criptografia,... a segurança de nível de linha) e é altamente recomendável toouse esse recurso em conjunto com eles além em ordem toobetter proteger dados confidenciais Olá Olá banco de dados. Observe que esse recurso tem suporte apenas a partir do SQL Server 2016 e do Banco de Dados SQL do Azure. |

## <a id="salted-hash"></a>Garantir que as senhas sejam armazenadas em um formato hash salgado

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Hash de senha usando APIs de criptografia do .NET](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Etapas** | As senhas não devem ser armazenadas em bancos de dados de repositório de usuários personalizados. Os hashes de senha devem ser armazenados com valores de sal em vez disso. Certifique-se de salt Olá para usuário Olá sempre é exclusiva e aplicar crypt b, s cript ou PBKDF2 antes de armazenar a senha hello, com uma contagem de iteração de fator de trabalho mínimo de 150.000 loops tooeliminate possibilidade de saudação de força bruta.| 

## <a id="db-encrypted"></a>Garantir que os dados confidenciais nas colunas do banco de dados sejam criptografados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Versão do SQL - Todas |
| **Referências**              | [Criptografando dados confidenciais no SQL Server](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [Como: criptografar uma coluna de dados no SQL Server](https://msdn.microsoft.com/library/ms179331), [Criptografar por certificado](https://msdn.microsoft.com/library/ms188061) |
| **Etapas** | Dados confidenciais, como números de cartão de crédito tem toobe criptografado no banco de dados de saudação. Dados podem ser criptografados usando a criptografia de nível de coluna ou por uma função de aplicativo usando as funções de criptografia de saudação. |

## <a id="tde-enabled"></a>Garantir que a criptografia no nível do banco de dados (TDE) esteja habilitada

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Noções básicas sobre a TDE (Transparent Data Encryption) do SQL Server](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Etapas** | Criptografia de dados transparente (TDE) de recursos no SQL server, ajuda a criptografar dados confidenciais em um banco de dados e proteger as chaves de hello são usadas tooencrypt Olá dados com um certificado. Isso impede que alguém sem as chaves de saudação usando dados de saudação. TDE protege os dados "em repouso", que significa que os arquivos de dados e de log hello. Ele fornece Olá capacidade toocomply com muitas leis, regulamentos e diretrizes estabelecidas em vários setores. |

## <a id="backup"></a>Garantir que os backups de banco de dados estejam criptografados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure, OnPrem |
| **Atributos**              | Versão do SQL - V12, Versão do SQL - MsSQL2014 |
| **Referências**              | [Criptografia do backup do banco de dados SQL](https://msdn.microsoft.com/library/dn449489) |
| **Etapas** | SQL Server tem dados de saudação do hello capacidade tooencrypt durante a criação de um backup. Especificando o algoritmo de criptografia hello e Criptografador hello (um certificado ou chave assimétrica) ao criar um backup, é possível criar um arquivo de backup criptografado. |

## <a id="api-browser"></a>Certifique-se de que tooWeb relevantes dados confidenciais que API não é armazenada no armazenamento do navegador

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC 5, MVC 6 |
| **Atributos**              | Provedor de Identidade - ADFS, Provedor de Identidade - Azure AD |
| **Referências**              | N/D  |
| **Etapas** | <p>Em determinadas implementações artefatos confidenciais relevantes tooWeb da API de autenticação são armazenados no armazenamento local do navegador. Por exemplo, os artefatos de autenticação do Azure AD, como adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key etc.</p><p>Todos esses artefatos estão disponíveis mesmo após sair ou depois que o navegador é fechado. Se um adversário obtém acesso a artefatos toothese, ele pode reutilizá-los tooaccess recursos de saudação protegido (APIs). Certifique-se de que todos os artefatos confidenciais tooWeb relacionados API não é armazenado no armazenamento do navegador. Em casos onde o armazenamento no lado do cliente é inevitável (por exemplo, única página de aplicativos (SPA) que aproveitam os fluxos de OpenIdConnect/OAuth implícita necessário toostore tokens de acesso localmente), use opções de armazenamento não tem a persistência. Por exemplo, prefira SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Exemplo
Olá JavaScript trecho abaixo é de uma biblioteca de autenticação personalizado que armazena os artefatos de autenticação no armazenamento local. Implementações desse tipo devem ser evitadas. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Criptografar dados confidenciais armazenados no Cosmos DB

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Azure Document DB | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Criptografe dados confidenciais no nível do aplicativo antes de armazenar em um banco de dados do documento ou de armazenar quaisquer dados confidenciais em outras soluções de armazenamento, como o Armazenamento do Azure ou o SQL Azure.| 

## <a id="disk-vm"></a>Usar discos de tooencrypt de criptografia de disco do Azure usados por máquinas virtuais

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança da VM da IaaS do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Usando a criptografia de disco do Azure tooencrypt discos usados por suas máquinas virtuais](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Etapas** | <p>O Azure Disk Encryption é um novo recurso que, atualmente, está na versão de visualização. Esse recurso permite que você tooencrypt Olá OS discos e dados usados por uma máquina Virtual IaaS. Para Windows, Olá unidades são criptografadas usando a tecnologia de criptografia do BitLocker padrão da indústria. Para o Linux, discos de saudação são criptografados usando a tecnologia de saudação DM Crypt. Isso é integrado com o Azure Key Vault tooallow você toocontrol e gerenciar chaves de criptografia de disco hello. Olá solução de criptografia de disco do Azure dá suporte a saudação três cenários de criptografia de cliente a seguir:</p><ul><li>Habilite a criptografia em novas VMs IaaS criadas de arquivos VHD criptografados pelo cliente e chaves de criptografia fornecidas pelo cliente, que são armazenados no Cofre de Chaves do Azure.</li><li>Habilite a criptografia em novas VMs de IaaS criado a partir de saudação do Azure Marketplace.</li><li>Habilite a criptografia em VMs IaaS existentes já em execução no Azure.</li></ul>| 

## <a id="fabric-apps"></a>Criptografar segredos nos aplicativos do Service Fabric

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de confiança do Service Fabric | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Ambiente - Azure |
| **Referências**              | [Gerenciando segredos em aplicativos do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Etapas** | Os segredos podem ser informações confidenciais, como cadeias de conexão de armazenamento, senhas ou outros valores que não devem ser tratados como texto sem formatação. Use o Azure Key Vault toomanage chaves e segredos em aplicativos de malha do serviço. |

## <a id="modeling-teams"></a>Executar a modelagem de segurança e usar unidades de negócios/equipes onde for necessário

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Execute a modelagem de segurança e use unidades de negócios/equipes onde for necessário. |

## <a id="entities"></a>Minimizar o recurso de tooshare de acesso em entidades críticos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Minimizar o recurso de tooshare de acesso em entidades críticos |

## <a id="good-practices"></a>Treinar os usuários Olá riscos associados ao recurso de compartilhamento do Dynamics CRM hello e boas práticas de segurança

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Treinar os usuários Olá riscos associados ao recurso de compartilhamento do Dynamics CRM hello e boas práticas de segurança |

## <a id="exception-mgmt"></a>Incluir uma regra de padrões de desenvolvimento que impeça a exibição dos detalhes de configuração do gerenciamento de exceções

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Inclua uma regra de padrões de desenvolvimento que impeça a exibição dos detalhes de configuração do gerenciamento de exceções. Teste isso como parte da inspeção periódica ou das revisões de código.|

## <a id="sse-preview"></a>Usar o Azure Storage Service Encryption (SSE) para dados em repouso (visualização)

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | StorageType - Blob |
| **Referências**              | [Criptografia do Serviço de Armazenamento do Azure para dados em repouso (visualização)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Etapas** | <p>Azure Storage Service criptografia (SSE) para dados em repouso ajuda você a proteger e proteger seu dados toomeet seu compromissos de conformidade e segurança da organização. Com esse recurso, o armazenamento do Azure automaticamente criptografa seu toostorage toopersisting anteriores de dados e descriptografa tooretrieval anterior. Olá criptografia, descriptografia e gerenciamento de chaves é toousers totalmente transparente. SSE aplica-se apenas o tooblock blobs, blobs de página e blobs de acréscimo. Olá outros tipos de dados, incluindo tabelas, filas e arquivos, não serão criptografados.</p><p>Fluxo de trabalho de criptografia e descriptografia:</p><ul><li>Prezado cliente habilita a criptografia na conta de armazenamento Olá</li><li>Quando o cliente Olá grava o novo armazenamento tooBlob de dados (Blob PUT, coloque o bloco, PUT Page, etc.); cada gravação é criptografada usando a criptografia AES de 256 bits, uma saudação mais fortes codificações em bloco disponíveis</li><li>Quando o cliente Olá precisa de dados de tooaccess (obter Blob, etc.), dados são automaticamente descriptografados antes de retornar o usuário toohello</li><li>Se a criptografia está desabilitada, novas gravações não são criptografadas e dados criptografados existentes permanecem criptografados até que recriado pelo usuário hello. Embora a criptografia estiver habilitada, gravações tooBlob armazenamento será criptografado. estado Olá dos dados não é alterada com usuário Olá alternando entre a habilitação e desabilitação de criptografia para a conta de armazenamento Olá</li><li>Todas as chaves de criptografia são armazenadas, criptografadas e gerenciadas pela Microsoft.</li></ul><p>Observe que, neste momento, as chaves de saudação usadas para criptografia de saudação são gerenciadas pela Microsoft. Microsoft gera chaves de saudação originalmente e gerenciar de armazenamento seguro de chaves hello, bem como rotação regular Olá Olá conforme definido pela política interna do Microsoft. Olá futuras, os clientes obterá Olá capacidade toomanage seus próprios > chaves de criptografia e forneça um caminho de migração de chaves gerenciados pelo Microsoft chaves toocustomer gerenciados.</p>| 

## <a id="client-storage"></a>Usar dados confidenciais do cliente criptografia toostore no armazenamento do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Criptografia no cliente e Azure Key Vault para o Armazenamento do Microsoft Azure](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Tutorial: criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Armazenando dados com segurança no Armazenamento de Blobs do Azure com as extensões de criptografia do Azure](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Etapas** | <p>Olá biblioteca de cliente de armazenamento do Azure para o pacote Nuget .NET oferece suporte a criptografia de dados em aplicativos cliente antes de carregar tooAzure armazenamento e a descriptografia de dados durante o download do cliente toohello. biblioteca de saudação também oferece suporte à integração com o Cofre de chaves do Azure para gerenciamento de chaves de conta de armazenamento. Aqui está uma breve descrição de como funciona a criptografia do lado do cliente:</p><ul><li>SDK de cliente de armazenamento do Azure Hello gera uma chave de criptografia do conteúdo (CEK), que é uma chave simétrica do uso de uma vez</li><li>Os dados do cliente são criptografados com essa CEK</li><li>Olá CEK é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e podem ser gerenciado localmente ou armazenada no cofre de chaves do Azure. cliente de armazenamento Olá próprio nunca tem acesso toohello KEK. Ele apenas invoca o algoritmo de chave encapsulamento Olá fornecida pelo Cofre de chaves. Os clientes podem escolher toouse a provedores personalizados para a chave encapsulamento/desencapsulamento se quiserem</li><li>Olá os dados criptografados são, em seguida, carregar toohello serviço de armazenamento do Azure. Verifique os links Olá na seção de referências de saudação para obter detalhes de implementação de baixo nível.</li></ul>|

## <a id="pii-phones"></a>Criptografar confidenciais ou dados PII gravados armazenamento local toophones

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvel | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genéricas, Xamarin  |
| **Atributos**              | N/D  |
| **Referências**              | [Gerenciar configurações e recursos em dispositivos com as políticas do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Keychain Valet](https://components.xamarin.com/view/square.valet) |
| **Etapas** | <p>Se o aplicativo hello grava informações confidenciais, como informações de identificação pessoal do usuário (email, número de telefone, nome, sobrenome, preferências etc.) -no sistema de arquivos do mobile, em seguida, ele deve ser criptografado antes de gravar toohello sistema de arquivos local. Se o aplicativo hello é um aplicativo corporativo, em seguida, explore possibilidade de saudação do aplicativo de publicação usando o Windows Intune.</p>|

### <a name="example"></a>Exemplo
Intune pode ser configurado com segurança políticas toosafeguard confidenciais dados a seguir: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Exemplo
Se o aplicativo hello não é um aplicativo corporativo e use plataforma fornecido keystore, chaves de criptografia toostore conjuntos de chaves, usando a operação de criptografia que podem ser executadas no sistema de arquivo hello. Código a seguir trecho mostra como tooaccess chave do conjunto de chaves usando o xamarin: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Ofuscar binários gerados antes de distribuir tooend usuários

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvel | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Crypto Obfuscator para .NET](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Etapas** | Gerado binários (assemblies apk) devem ser ofuscado toostop inversa de engenharia de assemblies. Ferramentas como o `CryptoObfuscator` pode ser usado para essa finalidade. |

## <a id="cert"></a>Conjunto clientCredentialType tooCertificate ou do Windows

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | Usando um UsernameToken com uma senha de texto sem formatação em um canal não criptografado expõe Olá senha tooattackers que pode detectar as mensagens de saudação do SOAP. Provedores de serviços que usam Olá UsernameToken pode aceitar senhas enviadas em texto não criptografado. Enviar senhas de texto sem formatação por um canal não criptografado pode expor Olá credencial tooattackers que pode detectar a mensagem de saudação do SOAP. | 

### <a name="example"></a>Exemplo
Olá seguinte configuração do provedor de serviço WCF usa Olá UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Definir clientCredentialType tooCertificate ou do Windows. 

## <a id="security"></a>O modo de segurança do WCF não está habilitado

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, .NET Framework 3 |
| **Atributos**              | Modo de segurança - Transport, Modo de segurança - Message |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html), [Noções básicas da segurança do WCF (CoDe Magazine)](http://www.codemag.com/article/0611051) |
| **Etapas** | Nenhuma segurança foi definida para transporte ou mensagens. Aplicativos que transmitem mensagens sem transporte ou mensagem de segurança não pode garantir a integridade de saudação ou confidencialidade de mensagens de saudação. Quando uma associação de segurança do WCF é definida tooNone, segurança de transporte e de mensagem estão desabilitados. |

### <a name="example"></a>Exemplo
Olá configuração a seguir define Olá tooNone de modo de segurança. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Exemplo
Há cinco modos de segurança disponíveis para todas as associações de serviço, são eles: 
* Nenhuma. desativa a segurança. 
* Transport: usa a segurança de transporte para a proteção de autenticações e mensagens. 
* Message. usa a segurança de mensagem para a proteção de autenticações e mensagens. 
* Both: Permite que você toosupply configurações de transporte e segurança em nível de mensagens (MSMQ só dá suporte a isso). 
* TransportWithMessageCredential: As credenciais são transmitidas com mensagem de saudação e proteção de mensagem e autenticação de servidor são fornecidos pela camada de transporte hello. 
* TransportCredentialOnly: As credenciais do cliente são passadas com a camada de transporte hello e nenhuma proteção de mensagem é aplicada. Use o transporte e segurança tooprotect Olá integridade de mensagens e a confidencialidade das mensagens. configuração de saudação abaixo informa Olá serviço toouse TLS com credenciais de mensagem.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
