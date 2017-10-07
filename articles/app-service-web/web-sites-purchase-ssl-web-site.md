---
title: "aaaAdd um SSL certificado tooyour aplicativo de serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como tooadd um SSL certificado tooyour aplicativo de serviço de aplicativo."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Comprar e configurar um certificado SSL para seu Serviço de Aplicativo do Azure

Neste tutorial, você irá proteger seu aplicativo web com a compra de um certificado SSL para o  **[serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714)** armazená-los em segurança no [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associá-lo a um domínio personalizado.

## <a name="step-1---log-in-tooazure"></a>Etapa 1 - Log em tooAzure

Faça logon no toohello portal do Azure em http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Etapa 2: Fazer um pedido de certificado SSL

Você pode colocar um pedido de certificado SSL, criando um novo [certificado de serviço de aplicativo](https://portal.azure.com/#create/Microsoft.SSL) em Olá **portal do Azure**.

![Criação de certificado](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Insira um amigável **nome** para o SSL de certificado e insira Olá **nome de domínio**

> [!NOTE]
> Esta é uma das partes mais importantes de saudação do processo de compra de saudação. Verifique se tooenter corrija o nome do host (domínio personalizado) que você deseja tooprotect com esse certificado. **NÃO** acrescentar o nome de Host de saudação com WWW. 
>

Selecione seu **assinatura**, **grupo de recursos**, e **SKU de certificado**

> [!WARNING]
> Certificados de serviço de aplicativo só pode ser usados por outros serviços de aplicativo no hello mesma assinatura.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Etapa 3 - certificado de saudação do repositório no cofre de chaves do Azure

> [!NOTE]
> O [Cofre da Chave](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem.
>

Após a conclusão da saudação aquisição do certificado SSL, você precisa tooopen [certificados de serviço de aplicativo](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) folha de recursos.

![Inserir imagem de toostore pronto em KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Você observará que o status do certificado é **"Emissão pendente"** , há algumas etapas mais precisar toocomplete antes de começar a usar este certificado.

Clique em **configuração do certificado** dentro de folha de propriedades do certificado e clique em **etapa 1: armazenamento** toostore esse certificado no cofre de chaves do Azure.

De **Status cofre da chave** folha, clique em **chave cofre repositório** toochoose um toostore de Cofre de chaves existente esse certificado **ou criar novo cofre de chaves** toocreate nova chave de cofre dentro da mesmo assinatura e grupo de recursos.

> [!NOTE]
> O cofre da chave do Azure tem encargos mínimo para armazenar o certificado.
> Para obter mais informações, consulte  **[detalhes de preços do Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Depois de selecionar Olá repositório de Cofre de chave toostore esse certificado no, Olá **repositório** opção deve mostrar o êxito.

![Inserir imagem de sucesso de repositório em KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Etapa 4 - verificar Olá propriedade do domínio

> [!NOTE]
> Há três tipos de verificação de domínio de certificados de serviço de aplicativo com suporte: verificação do domínio, email, Manual. Essas são explicadas em mais detalhes no hello [avançado seção](#advanced).

De Olá mesmo **configuração do certificado** folha que você usou na etapa 3, clique em **etapa 2: Verifique se**.

**Verificação de domínio** este é o processo mais conveniente Olá **somente se** tiver  **[comprado seu domínio personalizado de serviço de aplicativo do Azure.](custom-dns-web-site-buydomains-web-app.md)**
Clique em **verificar** botão toocomplete nesta etapa.

![Inserir imagem de verificação de domínio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Depois de clicar em **verificar**, use Olá **atualizar** botão até Olá **verificar** opção deve mostrar o êxito.

![Inserir imagem de verificar o êxito na KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Etapa 5: atribuir tooApp de certificado do serviço de aplicativo

> [!NOTE]
> Antes de executar as etapas de saudação nesta seção, você deve ter associado um nome de domínio personalizado com seu aplicativo. Para saber mais, confira **[Configurando um nome de domínio personalizado para um aplicativo Web.](app-service-web-tutorial-custom-domain.md)**
>

Em hello  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicativo** opção esquerda Olá da página de saudação.

Clique em nome de saudação de seu aplicativo toowhich você deseja tooassign esse certificado.

Em Olá **configurações**, clique em **certificados SSL**.

Clique em **Importar certificado de serviço de aplicativo** e selecione Olá certificado que você acabou de adquirir.

![inserir imagem de Importar Certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

Em hello **associações ssl** seção clique **adicionar associações**, usar toosecure de nome de domínio Olá menus suspensos tooselect Olá com SSL e Olá toouse do certificado. Você também pode selecionar se toouse  **[indicação de nome de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL baseado em IP.

![inserir imagem de Associações SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Clique em **Adicionar associação** toosave Olá alterações e habilitar o SSL.

> [!NOTE]
> Se você selecionou **SSL baseado em IP** e seu domínio personalizado está configurado para usar um registro, você deve executar etapas adicionais de saudação. Essas são explicadas em mais detalhes no hello [avançado seção](#Advanced).

Neste ponto, você deve ser capaz de toovisit seu aplicativo usando `HTTPS://` em vez de `HTTP://` tooverify que Olá certificado foi configurado corretamente.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Etapa 6 – Tarefas de gerenciamento

### <a name="azure-cli"></a>CLI do Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Avançado

### <a name="verifying-domain-ownership"></a>Verificando a propriedade de domínio

Há dois outros tipos de suporte para certificados de serviço do aplicativo de verificação de domínio: Mail e Verificação Manual.

#### <a name="mail-verification"></a>Verificação por email

Toohello que endereços de Email associados com este domínio personalizado já foi enviado ao email de verificação.
etapa de verificação de Email do toocomplete Olá, abra o email de saudação e clique em link de verificação de saudação.

![Inserir imagem de verificação de email](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Se você precisar de email de verificação tooresend hello, clique em Olá **reenviar Email** botão.

#### <a name="manual-verification"></a>Verificação manual

> [!IMPORTANT]
> Verificação da página da Web em HTML (funciona somente com SKU de Certificado Padrão)
>

1. Crie um arquivo HTML chamado **"starfield.html"**

1. Conteúdo desse arquivo deve ser nome exato de saudação do hello Token de verificação do domínio. (Você pode copiar token Olá de saudação folha de Status de verificação de domínio)

1. Carregue esse arquivo na raiz de saudação do servidor de web hello hospede seu domínio`/.well-known/pki-validation/starfield.html`

1. Clique em **atualizar** tooupdate status do certificado Olá após a conclusão da verificação. Pode levar alguns minutos para toocomplete de verificação.

> [!TIP]
> Verifique se um terminal usando `curl -G http://<domain>/.well-known/pki-validation/starfield.html` resposta Olá deve conter Olá `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Verificação de registro TXT do DNS

1. Usando o Gerenciador de DNS, criar um registro TXT no hello `@` subdomínio com toohello igual do valor o Token de verificação do domínio.
1. Clique em **"Atualizar"** tooupdate Olá após a conclusão da verificação de status do certificado.

> [!TIP]
> Você precisa de um registro TXT do toocreate em `@.<domain>` com valor `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Atribuir tooApp de certificado do serviço de aplicativo

Se você selecionou **SSL baseado em IP** e seu domínio personalizado está configurado para usar um registro, você deve executar etapas adicionais de saudação:

Depois que você configurou associação SSL com base em um IP, um endereço IP dedicado é atribuído tooyour aplicativo. Você pode encontrar esse endereço IP em Olá **domínio personalizado** página em configurações do aplicativo, imediatamente acima Olá **nomes de host** seção. Ele é listado como **endereço IP externo**

![inserir imagem de IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Observe que esse endereço IP é diferente do endereço IP virtual de saudação usado anteriormente registro Olá tooconfigure para seu domínio. Se você estiver configurado toouse SSL baseado em SNI ou não configurado toouse SSL, nenhum endereço será listado para esta entrada.

Usando ferramentas de saudação fornecidas por seu registrador de nome de domínio, modificar Olá um registro para o endereço IP do domínio personalizado nome toopoint toohello da etapa anterior hello.

## <a name="rekey-and-sync-hello-certificate"></a>Rechavear e sincronização Olá certificado

Se você alguma vez precisar tooRekey seu certificado, selecione **rechavear e sincronização** opção **propriedades do certificado** folha.

Clique em **rechavear** botão tooinitiate processo de saudação. Esse processo pode levar de 1 a 10 minutos toocomplete.

![inserir imagem de Nova Chave SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Seu certificado de troca de chaves faz o certificado de saudação com um novo certificado emitido da autoridade de certificação de saudação.

## <a name="next-steps"></a>Próximas etapas

* [Adicionar uma rede de fornecimento de conteúdo](app-service-web-tutorial-content-delivery-network.md)