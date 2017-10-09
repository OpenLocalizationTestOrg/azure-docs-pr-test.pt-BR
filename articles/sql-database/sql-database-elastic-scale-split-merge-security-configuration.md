---
title: "configuração de segurança de mesclagem aaaSplit | Microsoft Docs"
description: Configurar certificados x409 para criptografia
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Configuração de segurança da divisão e mesclagem
serviço de divisão/mesclagem de saudação toouse, você deve configurar corretamente segurança. serviço de saudação é parte do recurso de escala elástica de saudação do banco de dados SQL do Microsoft Azure. Para saber mais, confira o [Tutorial do serviço de divisão e mesclagem da escala elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Configurando certificados
Os certificados são configurados de duas maneiras. 

1. [Olá tooConfigure certificado SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure certificados de cliente](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain certificados
Certificados podem ser obtidos de autoridades de certificação pública (CAs) ou de saudação [o serviço de certificado do Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Esses são Olá preferido métodos tooobtain certificados.

Se essas opções não estiverem disponíveis, você pode gerar **certificados autoassinados**.

## <a name="tools-toogenerate-certificates"></a>Certificados de toogenerate de ferramentas
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>ferramentas de saudação toorun
* De um Prompt de Comando do Desenvolvedor para o Visual Studio, consulte o [Prompt de Comando do Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Se instalado, vá para:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Obter Olá WDK do [Windows 8.1: baixar kits e ferramentas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certificado SSL Olá tooconfigure
Um certificado SSL é necessário tooencrypt Olá comunicação e autenticar o servidor de saudação. Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:

### <a name="create-a-new-self-signed-certificate"></a>Criar um Novo certificado autoassinado
1. [Criar um certificado autoassinado](#create-a-self-signed-certificate)
2. [Criar o arquivo PFX para o certificado SSL autoassinado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
4. [Atualizar o certificado SSL no arquivo de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)
5. [Importar a autoridade de certificação SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>repositório de um certificado existente do certificado Olá toouse
1. [Exportar o certificado SSL do repositório de certificados](#export-ssl-certificate-from-certificate-store)
2. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
3. [Atualizar o certificado SSL no arquivo de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse um certificado existente em um arquivo PFX
1. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
2. [Atualizar o certificado SSL no arquivo de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certificados de cliente tooconfigure
Certificados de cliente são necessários na ordem tooauthenticate solicitações toohello serviço. Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:

### <a name="turn-off-client-certificates"></a>Desabilitar certificados de cliente
1. [Desabilitar a autenticação baseada em certificado do cliente](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Emitir novos certificados de cliente autoassinados
1. [Criar uma Autoridade de certificado autoassinado](#create-a-self-signed-certification-authority)
2. [Carregar certificado de autoridade de certificação tooCloud serviço](#upload-ca-certificate-to-cloud-service)
3. [Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço](#update-ca-certificate-in-service-configuration-file)
4. [Emitir certificados de cliente](#issue-client-certificates)
5. [Criar arquivos PFX para certificados de cliente](#create-pfx-files-for-client-certificates)
6. [Importar o certificado de cliente](#Import-Client-Certificate)
7. [Copie as impressões digitais de certificados de cliente](#copy-client-certificate-thumbprints)
8. [Configurar clientes permitido no hello arquivo de configuração de serviço](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Usar certificados de cliente existente
1. [Find CA Public Key](#find-ca-public-key)
2. [Carregar certificado de autoridade de certificação tooCloud serviço](#Upload-CA-certificate-to-cloud-service)
3. [Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Copie as impressões digitais de certificados de cliente](#Copy-Client-Certificate-Thumbprints)
5. [Configurar clientes permitido no hello arquivo de configuração de serviço](#configure-allowed-clients-in-the-service-configuration-file)
6. [Configurar a verificação de revogação de certificado do cliente](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Pontos de extremidade de serviço de toohello acesso podem ser restrita toospecific intervalos de endereços IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>criptografia tooconfigure para armazenamento de saudação
Um certificado é necessário tooencrypt credenciais de Olá que são armazenadas no repositório de metadados de saudação. Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:

### <a name="use-a-new-self-signed-certificate"></a>Usar um novo certificado autoassinado
1. [Criar um certificado autoassinado](#create-a-self-signed-certificate)
2. [Criar arquivo PFX de certificado de criptografia autoassinado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Carregar certificado de criptografia tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
4. [Atualizar o certificado de criptografia no arquivo de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Usar um certificado existente do repositório de certificados Olá
1. [Exportar o certificado de criptografia do repositório de certificados](#export-encryption-certificate-from-certificate-store)
2. [Carregar certificado de criptografia tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
3. [Atualizar o certificado de criptografia no arquivo de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Usar um certificado existente em um arquivo PFX
1. [Carregar certificado de criptografia tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
2. [Atualizar o certificado de criptografia no arquivo de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>configuração padrão de saudação
configuração padrão de saudação nega o ponto de extremidade HTTP toohello de todos os acesso. Isso é hello recomendado de configuração, como pontos de extremidade do hello solicitações toothese podem carregar informações confidenciais, como credenciais de banco de dados.
configuração padrão de saudação permite que o ponto de extremidade HTTPS toohello de todos os acesso. Essa configuração pode ser mais restrita.

### <a name="changing-hello-configuration"></a>Alterar configuração de saudação
Olá grupo de regras de controle de acesso que se aplicam a tooand de ponto de extremidade são configurados no hello  **<EndpointAcls>**  seção Olá **arquivo de configuração do serviço**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

regras de saudação em um grupo de controle de acesso são configuradas em um <AccessControl name=""> seção do arquivo de configuração do serviço de saudação. 

formato de saudação é explicado na documentação de listas de controle de acesso à rede.
Por exemplo, tooallow apenas IPs em Olá intervalo 100.100.0.0 too100.100.255.255 tooaccess Olá ponto de extremidade HTTPS, regras de saudação teria esta aparência:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Negação de prevenção de serviço
Há dois mecanismos diferentes suporte toodetect e evitar ataques de negação de serviço:

* Restringir o número de solicitações simultâneas por host remoto (desativado por padrão)
* Restringir a taxa de acesso por host remoto (em por padrão)

Eles se baseiam em recursos hello mais documentados na segurança de IP dinâmico no IIS. Ao alterar essa configuração tenha cuidado com hello fatores a seguir:

* comportamento de saudação de proxies e dispositivos de conversão de endereços de rede sobre informações de host remoto Olá
* Cada recurso de tooany de solicitação em função da web de saudação é considerado (por exemplo, carregar scripts, imagens, etc)

## <a name="restricting-number-of-concurrent-accesses"></a>Restringir o número de acessos simultâneos
configurações de saudação que configurar esse comportamento são:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Altere DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable essa proteção.

## <a name="restricting-rate-of-access"></a>Restringindo a taxa de acesso
configurações de saudação que configurar esse comportamento são:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Configurar Olá resposta tooa negou a solicitação
Olá configuração a seguir configura Olá resposta tooa negada a solicitação:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Consulte a documentação do toohello para outros valores com suporte para segurança de IP dinâmico no IIS.

## <a name="operations-for-configuring-service-certificates"></a>Operações para configurar certificados de serviço
Este tópico é apenas para referência. Siga etapas de configuração de saudação descritas no:

* Configurar o certificado SSL Olá
* Configurar certificados de cliente

## <a name="create-a-self-signed-certificate"></a>Criar um certificado autoassinado
Execute:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* URL do serviço - n com hello. Há suporte para caracteres curinga ("CN=*.cloudapp .net") e nomes alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").
* -e com data de validade do certificado Olá criar uma senha forte e especificá-lo quando solicitado.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Criar o arquivo PFX para o certificado SSL autoassinado
Execute:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Digite a senha e, em seguida, exporte o certificado com as seguintes opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades estendidas

## <a name="export-ssl-certificate-from-certificate-store"></a>Exportar o certificado SSL do repositório de certificados
* Localize o certificado
* Clique em Ações -> todas as tarefas -> Exportar...
* Exportar o certificado em um arquivo .PFX com as seguintes opções:
  * Sim, exportar a chave privada Olá
  * Incluir todos os certificados no caminho de certificação Olá se possível * exportar todas as propriedades estendidas

## <a name="upload-ssl-certificate-toocloud-service"></a>Carregar o serviço de toocloud de certificado SSL
Carregue o certificado com hello existente ou gerado. Arquivo PFX com hello par de chaves SSL:

* Digite a senha de saudação protegendo informações de chave privada Olá

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Atualizar o certificado SSL no arquivo de configuração de serviço
Atualize o valor de impressão digital de saudação do hello após a configuração no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Importar a autoridade de certificação SSL
Siga estas etapas em todas as contas/máquina que irá se comunicar com o serviço de saudação:

* Clique duas vezes em hello. Arquivo CER no Windows Explorer
* Na caixa de diálogo de certificado hello, clique em Instalar certificado...
* Importar o certificado para Olá que repositório de autoridades de certificação raiz confiáveis

## <a name="turn-off-client-certificate-based-authentication"></a>Desabilitar a autenticação baseada em certificado do cliente
Somente o cliente baseada em certificado autenticação tem suporte e desabilitá-lo permitirá acesso público toohello pontos de extremidade, a menos que outros mecanismos estão em vigor (por exemplo, Microsoft Azure Virtual Network).

Altere toofalse essas configurações no recurso de saudação tooturn do arquivo de configuração de serviço Olá:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Em seguida, copie Olá mesma impressão digital que Olá SSL de certificado na configuração da saudação da autoridade de certificação do certificado:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Criar uma Autoridade de certificado autoassinado
Execute Olá seguindo as etapas toocreate tooact um certificado autoassinado como uma autoridade de certificação:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize-lo

* -e com a data de expiração da certificação de saudação

## <a name="find-ca-public-key"></a>Localizar a chave pública da autoridade de certificação
Todos os certificados de cliente devem ter sido emitidos por uma autoridade de certificação confiável pelo serviço de saudação. Localize toohello chave pública Olá autoridade de certificação que emitiu os certificados de cliente de saudação que serão toobe usado para autenticação no tooupload ordem-toohello serviço de nuvem.

Se o arquivo hello com a chave pública Olá não estiver disponível, você deve exportá-lo saudação do repositório de certificados:

* Localize o certificado
  * Olá de procurar por um certificado de cliente emitido pela mesma autoridade de certificação
* Clique duas vezes no certificado de saudação.
* Selecione a guia de caminho de certificação de saudação na caixa de diálogo de certificado hello.
* Clique duas vezes em entrada de autoridade de certificação Olá no caminho de saudação.
* Fazer anotações de propriedades do certificado hello.
* Olá fechar **certificado** caixa de diálogo.
* Localize o certificado
  * Pesquisar Olá observada acima da autoridade de certificação.
* Clique em Ações -> todas as tarefas -> Exportar...
* Exportar o certificado em um .CER com as seguintes opções:
  * **Não, não exportar chave privada Olá**
  * Inclua todos os certificados no caminho de certificação hello, se possível.
  * Exportar todas as propriedades estendidas.

## <a name="upload-ca-certificate-toocloud-service"></a>Carregar o serviço de toocloud de certificado de autoridade de certificação
Carregue o certificado com hello existente ou gerado. Arquivo CER com a chave pública de saudação da autoridade de certificação.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço
Atualize o valor de impressão digital de saudação do hello após a configuração no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Atualizar o valor Olá Olá após a configuração com hello mesmo impressão digital:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Emitir certificados de cliente
Cada serviço de saudação individuais tooaccess autorizados deve ter um certificado de cliente emitido para his/hers exclusivo a usar e deve escolher que HIS/hers possui senha forte tooprotect sua chave privada. 

Olá, as etapas a seguir deve ser executado no hello mesma máquina onde Olá autoassinado certificado de autoridade de certificação foi gerada e armazenada:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Personalizando:

* -n com uma ID de cliente toohello que será autenticado com o certificado
* -e com data de validade do certificado Olá
* MyID.pvk e MyID.cer com nomes de arquivo exclusivo para o certificado de cliente

Esse comando solicitará um toobe senha criada e usada uma vez. Use uma senha forte.

## <a name="create-pfx-files-for-client-certificates"></a>Criar arquivos PFX para certificados de cliente
Para cada certificado de cliente gerado, execute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizando:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Digite a senha e, em seguida, exporte o certificado com as seguintes opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades estendidas
* Olá toowhom individuais que esse certificado está sendo emitido deve escolher uma senha de exportação Olá

## <a name="import-client-certificate"></a>Importar o certificado de cliente
Cada pessoa para quem um certificado de cliente tiver sido emitido deve importar o par de chaves Olá máquinas hello, ele usará toocommunicate com o serviço de saudação:

* Clique duas vezes em hello. Arquivo PFX no Windows Explorer
* Importar o certificado para Olá pessoal armazenar pelo menos essa opção:
  * Incluir todas as propriedades estendidas marcadas

## <a name="copy-client-certificate-thumbprints"></a>Copie as impressões digitais de certificados de cliente
Cada pessoa para quem um certificado de cliente tiver sido emitido deve seguir estas etapas na ordem tooobtain Olá impressão digital his/hers certificado que será adicionado toohello arquivo de configuração de serviço:

* Executar certmgr.exe
* Selecione a guia pessoal Olá
* Clique duas vezes no certificado do cliente Olá toobe usado para autenticação
* Olá certificado caixa de diálogo que é aberta, selecione a guia de detalhes de saudação
* Certifique-se de que mostrar está exibindo todos
* Campo de saudação selecione denominado impressão digital na lista de saudação
* Copiar valor Olá da impressão digital de saudação do * * excluir os caracteres Unicode não visíveis na frente do primeiro dígito de hello * * excluir todos os espaços

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Configurar clientes de permitido no arquivo de configuração de serviço Olá
Atualize o valor de saudação do hello configuração no arquivo de configuração de serviço Olá com uma lista separada por vírgulas de impressões digitais de Olá Olá certificados de cliente permitidos acesso toohello serviço a seguir:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Configurar a verificação de revogação de certificado do cliente
não verifica a configuração padrão de saudação com hello autoridade de certificação para o status de revogação de certificado de cliente. tooturn em Olá verifica se Olá autoridade de certificação que emitiu os certificados de cliente Olá dá suporte a essas verificações, altere Olá após a configuração com um dos valores hello definidos no hello enumeração X509RevocationMode:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Criar arquivo PFX para certificados de criptografia autoassinados
Para um certificado de criptografia, execute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizando:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Digite a senha e, em seguida, exporte o certificado com as seguintes opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades estendidas
* Você precisará senha Olá ao carregar o serviço de nuvem Olá certificado toohello.

## <a name="export-encryption-certificate-from-certificate-store"></a>Exportar o certificado de criptografia do repositório de certificados
* Localize o certificado
* Clique em Ações -> todas as tarefas -> Exportar...
* Exportar o certificado em um arquivo .PFX com as seguintes opções: 
  * Sim, exportar a chave privada Olá
  * Incluir todos os certificados no caminho de certificação hello, se possível 
* Exportar todas as propriedades estendidas

## <a name="upload-encryption-certificate-toocloud-service"></a>Carregar o serviço de toocloud de certificado de criptografia
Carregue o certificado com hello existente ou gerado. Arquivo PFX com o par de chaves de criptografia de saudação:

* Digite a senha de saudação protegendo informações de chave privada Olá

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Atualizar o certificado de criptografia no arquivo de configuração de serviço
Atualize o valor de impressão digital de saudação do hello configurações no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem a seguir:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Operações comuns de certificado
* Configurar o certificado SSL Olá
* Configurar certificados de cliente

## <a name="find-certificate"></a>Localize o certificado
Siga estas etapas:

1. Execute mmc.exe.
2. Arquivo -> Adicionar/Remover Snap-in...
3. Selecione **Certificados**.
4. Clique em **Adicionar**.
5. Escolha o local de repositório de certificados de saudação.
6. Clique em **Concluir**.
7. Clique em **OK**.
8. Expanda **Certificados**.
9. Expanda o nó de armazenamento de certificado hello.
10. Expanda Olá certificado filho.
11. Selecione um certificado na lista de saudação.

## <a name="export-certificate"></a>Exportar o certificado
Em Olá **Assistente para exportação de certificados**:

1. Clique em **Avançar**.
2. Selecione **Sim**, em seguida, **chave privada de saudação de exportação**.
3. Clique em **Avançar**.
4. Selecione o formato de arquivo de saída desejada hello.
5. Verifique as opções de saudação desejada.
6. Marque a **Senha**.
7. Digite uma senha forte e confirme-a.
8. Clique em **Avançar**.
9. Digite ou procure um nome de arquivo onde toostore Olá certificado (use um. Extensão PFX).
10. Clique em **Avançar**.
11. Clique em **Concluir**.
12. Clique em **OK**.

## <a name="import-certificate"></a>Importar certificado
Em Olá Assistente de importação de certificado:

1. Selecione o local do repositório de saudação.
   
   * Selecione **usuário atual** se apenas os processos em execução em usuário atual serão acessar o serviço de saudação
   * Selecione **Máquina Local** se outros processos no computador acessará o serviço Olá
2. Clique em **Avançar**.
3. Se estiver importando de um arquivo, confirme o caminho do arquivo hello.
4. Se estiver importando um arquivo .PFX:
   1. Digite a senha de saudação proteger a chave privada Olá
   2. Selecione as opções de importação
5. Selecionar certificados de "Local" em Olá repositório a seguir
6. Clique em **Procurar**.
7. Selecione repositório de saudação desejado.
8. Clique em **Concluir**.
   
   * Se o repositório de autoridade de certificação raiz confiável Olá foi escolhido, clique em **Sim**.
9. Clique em **OK** em todas as janelas de diálogo.

## <a name="upload-certificate"></a>Carregar um certificado
Em Olá [Portal do Azure](https://portal.azure.com/)

1. Selecione os **Serviços de nuvem**.
2. Selecione o serviço de nuvem hello.
3. Clique no menu superior Olá **certificados**.
4. Na barra inferior de saudação, clique em **carregar**.
5. Selecione o arquivo de certificado de saudação.
6. Se é um. PFX do arquivo, digite a senha de saudação para a chave privada hello.
7. Depois de concluído, copie impressão digital do certificado Olá da nova entrada na lista de saudação de hello.

## <a name="other-security-considerations"></a>Outras considerações de segurança
configurações de SSL Olá descritas neste documento criptografar a comunicação entre Olá serviço e seus clientes quando o ponto de extremidade HTTPS Olá é usado. Isso é importante, pois as credenciais para acesso de banco de dados e possivelmente, outras informações confidenciais estão contidos na comunicação hello. No entanto, observe que o serviço Olá persista status interno, incluindo credenciais, em suas tabelas internas no banco de dados de SQL do Microsoft Azure de saudação que você forneceu para o armazenamento de metadados na sua assinatura do Microsoft Azure. Esse banco de dados foi definido como parte da saudação após a configuração no arquivo de configuração do serviço (. Arquivo CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

As credenciais armazenadas neste banco de dados são criptografadas. No entanto, como uma prática recomendada, verifique se as funções web e de trabalho de suas implantações de serviço são atualizadas toodate e seguro como eles têm acesso toohello metadados hello e banco de dados do certificado usado para criptografia e descriptografia de credenciais armazenadas. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

