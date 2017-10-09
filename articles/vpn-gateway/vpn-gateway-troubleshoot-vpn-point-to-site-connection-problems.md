---
title: "problemas de conexão aaaTroubleshoot Azure ponto a site | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de conexão de ponto a site."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Solução de problemas: problemas de conexão de ponto a site do Azure

Este artigo lista os problemas comuns de conexão de ponto a site que podem ocorrer. Também discute as possíveis causas e soluções para esses problemas.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Erro de cliente VPN: não foi possível encontrar um certificado

### <a name="symptom"></a>Sintoma

Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:

**Não foi possível encontrar um certificado que possa ser usado com este protocolo EAP. (Erro 798)**

### <a name="cause"></a>Causa

Esse problema ocorre se o certificado de cliente hello está ausente no **certificados - certificados atual**.

### <a name="solution"></a>Solução

Verifique se que esse certificado de cliente hello está instalado no hello local do repositório de certificados da saudação (Certmgr.msc) a seguir:
 
**Certificates - Current User\Personal\Certificates**

Para obter mais informações sobre como tooinstall Olá certificado de cliente, consulte [gerar e exportar certificados para conexões ponto a site](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Quando você importa o certificado de cliente hello, não selecione Olá **habilitar a proteção forte de chave privada** opção.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Erro de cliente VPN: mensagem de saudação recebida era inesperada ou formatada incorretamente

### <a name="symptom"></a>Sintoma

Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:

**mensagem de saudação recebida era inesperada ou formatada incorretamente. (Erro 0x80090326)**

### <a name="cause"></a>Causa

Esse problema ocorre se a chave pública do certificado de raiz de saudação não é carregada no gateway de VPN do Azure hello. Ele também pode ocorrer se a chave hello está corrompido ou expirado.

### <a name="solution"></a>Solução

tooresolve esse problema, verificar o status de saudação da raiz de saudação do certificado em Olá toosee portal do Azure se ele foi revogado. Se não for revogado, tente reupload e certificado de raiz toodelete hello. Para saber mais, confira [Criar certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Erro de cliente VPN: uma cadeia de certificados foi processada, mas fechada 

### <a name="symptom"></a>Sintoma 

Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:

**Uma cadeia de certificados processada, mas terminou em um certificado raiz que não é confiável pelo provedor de confiança de saudação.**

### <a name="solution"></a>Solução

1. Certifique-se de que Olá certificados a seguir estão no local correto hello:

    | Certificado | Local padrão |
    | ------------- | ------------- |
    | AzureClient.pfx  | Current User\Personal\Certificates |
    | Azuregateway-*GUID*.cloudapp.net  | Current User\Trusted Root Certification Authorities|
    | AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer    | Local Computer\Trusted Root Certification Authorities|

2. Se certificados Olá já estão no local de hello, tente certificados de saudação toodelete e reinstalá-los. Olá  **azuregateway -*GUID*. cloudapp.net** certificado está no hello configuração pacote do cliente VPN que você baixou da saudação portal do Azure. Você pode usar archivers tooextract Olá arquivos do pacote de saudação.

## <a name="file-download-error-target-uri-is-not-specified"></a>Erro no download do arquivo: o URI de destino não foi especificado

### <a name="symptom"></a>Sintoma

Você receberá Olá a seguinte mensagem de erro:

**Erro de download do arquivo. O URI de destino não foi especificado.**

### <a name="cause"></a>Causa 

Esse problema ocorre devido ao tipo de gateway incorreto. 

### <a name="solution"></a>Solução

Olá tipo de gateway VPN deve ser **VPN**, e deve ser Olá tipo VPN **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Erro de cliente VPN: falha de script personalizado do VPN Azure 

### <a name="symptom"></a>Sintoma

Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:

**Script personalizado (tooupdate sua tabela de roteamento) falhou. (Erro 8007026f)**

### <a name="cause"></a>Causa

Esse problema pode ocorrer se você estiver tentando conexão de VPN tooopen Olá ponto a site usando um atalho.

### <a name="solution"></a>Solução 

Abra o pacote VPN de saudação diretamente, em vez de abri-lo do atalho hello.

## <a name="cannot-install-hello-vpn-client"></a>Não é possível instalar o cliente VPN Olá

### <a name="cause"></a>Causa 

Um certificado adicional será necessária tootrust gateway VPN Olá para sua rede virtual. Olá certificado está incluído no pacote configuração de cliente VPN de saudação que é gerado em Olá portal do Azure.

### <a name="solution"></a>Solução

Extraia o pacote de configuração de cliente VPN hello e localizar o arquivo. cer de saudação. Olá tooinstall do certificado, siga estas etapas:

1. Abra mmc.exe.
2. Adicionar Olá **certificados** snap-in.
3. Selecione Olá **computador** de conta de computador local hello.
4. Saudação de atalho **autoridades de certificação raiz confiáveis** nó. Clique em **todas as tarefas** > **importação**e procurar toohello. cer arquivos extraídos do pacote de configuração de cliente VPN hello.
5. Reinicie o computador de saudação. 
6. Tente tooinstall do cliente VPN hello.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Erro de portal do Azure: falha do gateway VPN toosave hello e dados saudação são inválidos

### <a name="symptom"></a>Sintoma

Quando você tenta toosave alterações de saudação de gateway VPN Olá Olá portal do Azure, você receberá Olá a seguinte mensagem de erro:

**Gateway de rede virtual com falha toosave &lt;* nome do gateway*&gt;. Os dados para o certificado &lt;*ID do certificado*&gt; são inválidos.**

### <a name="cause"></a>Causa 

Esse problema pode ocorrer se Olá raiz chave pública de certificado que você carregou contém um caractere inválido, como um espaço.

### <a name="solution"></a>Solução

Certifique-se de que dados Olá no certificado de saudação não contém caracteres inválidos, como quebras de linha (retorno de carro). valor inteiro Olá deve ser uma linha longa. Olá texto a seguir está um exemplo de certificado hello:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Erro de portal do Azure: falha do gateway VPN toosave hello e Olá nome do recurso é inválido

### <a name="symptom"></a>Sintoma

Quando você tenta toosave alterações de saudação de gateway VPN Olá Olá portal do Azure, você receberá Olá a seguinte mensagem de erro: 

**Gateway de rede virtual com falha toosave &lt;* nome do gateway*&gt;. Nome do recurso &lt; *nome do certificado que você tente tooupload* &gt; é inválido * *.

### <a name="cause"></a>Causa

Esse problema ocorre porque o nome de saudação do certificado Olá contém um caractere inválido, como um espaço. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Erro 503 de portal do Azure: erro de download do arquivo do pacote VPN

### <a name="symptom"></a>Sintoma

Ao testar o pacote de configuração de cliente VPN do toodownload hello, você recebe Olá a seguinte mensagem de erro:

**Falha ao arquivo de saudação toodownload. Detalhes do erro: erro 503. Olá servidor está ocupado.**
 
### <a name="solution"></a>Solução

Esse erro pode ser causado por um problema de rede temporário. Tente o pacote VPN Olá toodownload novamente após alguns minutos.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>A atualização de Gateway VPN do Azure: P2S todos os clientes são tooconnect não é possível

### <a name="cause"></a>Causa

Se o certificado Olá é mais de 50 por cento por meio de seu ciclo de vida, o certificado de saudação é rodado.

### <a name="solution"></a>Solução

tooresolve esse problema, crie e redistribuir novos clientes VPN toohello de certificados. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Muitos clientes VPN conectados ao mesmo tempo

Para cada gateway VPN, o número máximo de saudação de conexões permitidas é 128. Você pode ver o número total de saudação de clientes conectados em Olá portal do Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>VPN ponto a site incorretamente adiciona uma rota para a tabela de rotas toohello 10.0.0.0/8

### <a name="symptom"></a>Sintoma

Quando você discar Olá conexão VPN no cliente de ponto para site Olá, do cliente VPN Olá deve adicionar uma rota de rede virtual do Azure de saudação. serviço do auxiliar de IP Hello deve adicionar uma rota para a sub-rede de saudação de clientes VPN de saudação. 

Olá intervalo de cliente VPN pertence a menor sub-rede tooa 10.0.0.0/8 como 10.0.12.0/24. Em vez de uma rota para 10.0.12.0/24, é adicionada uma rota para 10.0.0.0/8 que tem prioridade mais alta. 

Essa rota incorreta quebras de conectividade com outras redes locais que podem pertencer a sub-rede tooanother dentro do intervalo de 10.0.0.0/8 hello, como 10.50.0.0/24, que não têm uma rota específica de definidos. 

### <a name="cause"></a>Causa

Esse comportamento ocorre por padrão para clientes do Windows. Quando Olá cliente usa o protocolo PPP IPCP Olá, ele obtém o endereço IP de Olá para interface de túnel de saudação do servidor de saudação (gateway VPN Olá neste caso). No entanto, devido a uma limitação no protocolo hello, o cliente de saudação não tem máscara de sub-rede de saudação. Porque não há nenhum outro tooget de maneira, cliente Olá tenta tooguess máscara de sub-rede de saudação com base na classe de saudação do endereço IP da interface de túnel hello. 

Portanto, é adicionada uma rota com base em Olá mapeamento estático a seguir: 

Se o endereço pertence A tooclass--> Aplicar /8

Se o endereço pertence tooclass--> B aplicar /16

Se o endereço pertence tooclass--> C aplicar /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>O cliente VPN não pode acessar compartilhamentos de arquivos de rede

### <a name="symptom"></a>Sintoma

cliente VPN Olá conectou toohello rede virtual do Azure. No entanto, o cliente Olá não pode acessar compartilhamentos de rede.

### <a name="cause"></a>Causa

Olá protocolo SMB é usado para acesso de compartilhamento de arquivos. Quando a conexão de saudação for iniciada, cliente VPN Olá adiciona credenciais de sessão de saudação e Olá falha ocorre. Depois de estabelecer conexão hello, cliente Olá é forçado toouse Olá cache as credenciais de autenticação Kerberos. Esse processo inicia consultas toohello Key Distribution Center (um controlador de domínio) tooget um token. Como cliente Olá se conecta de saudação à Internet, não pode ser tooreach capaz de controlador de domínio de saudação. Portanto, cliente Olá não é possível realizar failover da tooNTLM Kerberos. 

Olá apenas tempo que o cliente Olá é solicitado para uma credencial é quando ele tem um certificado válido (com SAN = UPN) emitido por Olá toowhich de domínio está associado. cliente Olá também deve ser conectada fisicamente toohello rede de domínio. Nesse caso, o cliente de Olá tenta toouse certificado de saudação e atinge toohello controlador de domínio. Olá Key Distribution Center retorna um erro de "KDC_ERR_C_PRINCIPAL_UNKNOWN". cliente de saudação é forçado toofail tooNTLM. 

### <a name="solution"></a>Solução

toowork problema hello, desabilitar o cache de saudação de credenciais de domínio de saudação seguinte subchave do registro: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Não é possível localizar a conexão de VPN de ponto para site Olá no Windows após a reinstalação do cliente VPN Olá

### <a name="symptom"></a>Sintoma

Remover conexão de VPN de ponto para site hello e, em seguida, reinstalar o cliente VPN hello. Nessa situação, Olá conexão VPN não está configurado com êxito. Você não vir a conexão de VPN Olá no hello **conexões de rede** configurações do Windows.

### <a name="solution"></a>Solução

problema de saudação tooresolve, excluir Olá antigo VPN cliente arquivos de configuração de **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, e execute o instalador do cliente VPN Olá novamente.
