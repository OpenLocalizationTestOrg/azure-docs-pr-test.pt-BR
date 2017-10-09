---
title: "aaaConfigure SSL para um serviço de nuvem (clássicos) | Microsoft Docs"
description: "Saiba como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configurando SSL para um aplicativo no Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [Portal clássico do Azure](cloud-services-configure-ssl-certificate.md)
> 
> 

Criptografia do Secure Socket Layer (SSL) é o método de hello mais comumente usada de proteção de dados enviados pela Olá internet. Essa tarefa comum discute como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo.

> [!NOTE]
> procedimentos de saudação nesta tarefa se aplicam a serviços de nuvem tooAzure; para serviços de aplicativos, consulte [isso](../app-service-web/web-sites-configure-ssl-certificate.md) artigo.
> 
> 

Essa tarefa usa uma implantação de produção. Informações sobre o uso de uma implantação de preparo são fornecidas no final deste tópico hello.

Leia [este](cloud-services-how-to-create-deploy.md) artigo primeiro se você ainda não tiver criado um serviço de nuvem.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Etapa 1: Obter um certificado SSL
tooconfigure SSL para um aplicativo, você primeiro precisa tooget um certificado SSL assinado por uma autoridade de certificação (CA), um terceiro confiável que emite certificados para essa finalidade. Se você ainda não tiver um, será necessário tooobtain uma empresa que vende certificados SSL.

certificado de saudação deve atender aos Olá seguindo os requisitos para certificados SSL no Azure:

* certificado de saudação deve conter uma chave privada.
* certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).
* Hello nome da entidade do certificado deve corresponder o serviço de nuvem do hello domínio usado tooaccess hello. Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio do hello cloudapp.net. Você deve adquirir um toouse de nome de domínio personalizado ao seu serviço de acesso. Quando você solicitar um certificado de uma autoridade de certificação, nome da entidade do certificado Olá deve corresponder Olá domínio personalizado nome usado tooaccess seu aplicativo. Por exemplo, se o nome de domínio personalizado for **contoso.com**, você pode solicitar um certificado da autoridade de certificação para ***.contoso.com** ou **www.contoso.com**.
* certificado Olá deve usar um mínimo de criptografia de 2048 bits.

Para fins de teste, você pode [criar](cloud-services-certs-create.md) e usar um certificado autoassinado. Um certificado autoassinado não é autenticado por meio de uma autoridade de certificação e pode usar o domínio cloudapp.net de saudação como Olá URL do site. Por exemplo, hello tarefa a seguir usa um certificado autoassinado no qual Olá nome comum (CN) utilizado no certificado de saudação é **sslexample.cloudapp.net**.

Em seguida, você deve incluir informações sobre o certificado de saudação em sua definição de serviço e arquivos de configuração de serviço.

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Etapa 2: Modificar arquivos de definição e configuração de serviço Olá
Seu aplicativo deve ser o certificado de saudação toouse configurado e um ponto de extremidade HTTPS deve ser adicionado. Como resultado, hello definição de serviço e arquivos de configuração de serviço necessário toobe atualizado.

1. Em seu ambiente de desenvolvimento, abra o arquivo de definição de serviço (CSDEF) hello, adicione um **certificados** seção dentro de saudação **WebRole** seção e incluir Olá informações a seguir o certificado (e certificados intermediários):
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   Olá **certificados** seção define o nome de saudação do nosso certificado, seu local e o nome de saudação do repositório Olá onde ele está localizado.
   
   Permissões (`permisionLevel` atributo) pode ser tooone de conjunto de saudação seguintes valores:
   
   | Valor da permissão | Descrição |
   | --- | --- |
   | limitedOrElevated |**(Padrão)**  Todos os processos de função podem acessar a chave privada hello. |
   | elevado |Somente os processos elevados podem acessar a chave privada hello. |
2. Em seu arquivo de definição de serviço, adicionar um **InputEndpoint** elemento dentro do hello **pontos de extremidade** seção tooenable HTTPS:
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. Em seu arquivo de definição de serviço, adicionar um **associação** elemento dentro do hello **Sites** seção. Esta seção adiciona uma associação de HTTPS toomap o site do ponto de extremidade tooyour:
   
    ```xml   
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   Arquivo de definição de todos os Olá alterações necessárias toohello serviço foram concluídas, mas ainda precisar de informações de certificado de saudação tooadd ao arquivo de configuração do serviço de saudação.
4. Em seu arquivo de configuração de serviço (CSCFG), ServiceConfiguration, adicione um **certificados** seção dentro de saudação **função** seção, substituindo o valor de impressão digital do exemplo hello mostrado abaixo com que do seu certificado:
   
    ```xml   
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(Olá precede o exemplo usa **sha1** para algoritmo de impressão digital de saudação. Especificar valor de saudação apropriado para o algoritmo de impressão digital do certificado).

Agora que os arquivos de configuração Olá serviço definição e o serviço foi atualizados, sua implantação para carregar tooAzure do pacote. Caso esteja usando **cspack**, não use o sinalizador **/generateConfigurationFile**, pois ele substituirá as informações de certificado que você acabou de inserir.

## <a name="step-3-upload-a-certificate"></a>Etapa 3: Carregar um certificado
O pacote de implantação foi atualizada toouse certificado de saudação e um ponto de extremidade HTTPS foi adicionado. Agora você pode carregar Olá tooAzure de pacote e o certificado com hello portal clássico do Azure.

1. Faça logon no toohello [portal clássico do Azure][Azure classic portal]. 
2. Clique em **serviços de nuvem** no painel de navegação do lado esquerdo da saudação.
3. Clique no serviço de nuvem Olá desejado.
4. Clique em Olá **certificados** guia.
   
    ![Clique em Guia de certificados Olá](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Clique em Olá **carregar** botão.
   
    ![Carregar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Fornecer Olá **arquivo**, **senha**, em seguida, clique em **concluir** (Olá a marca de seleção).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Etapa 4: Conectar a instância de função toohello usando HTTPS
Agora que sua implantação estiver em execução no Azure, você pode conectar tooit usando HTTPS.

1. Em Olá portal clássico do Azure, selecione sua implantação, clique em link Olá em **URL do Site**.
   
   ![Determinar URL do site][2]
2. No navegador da web, modifique Olá link toouse **https** em vez de **http**e, em seguida, visite a página de saudação.
   
   > [!NOTE]
   > Se você estiver usando um certificado autoassinado, quando você procurar o ponto de extremidade HTTPS de tooan associada com um certificado autoassinado hello, que você verá um erro de certificado no navegador de saudação. Usando um certificado assinado por uma autoridade de certificação confiável elimina esse problema; em Olá enquanto isso, você pode ignorar o erro de saudação. (Outra opção é o repositório de certificados do usuário do toohello certificado autoassinado Olá tooadd certificado confiável autoridade.)
   > 
   > 
   
   ![Site de exemplo SSL][3]

Se você quiser toouse SSL para uma implantação de preparo, em vez de uma implantação de produção, você primeiro precisa toodetermine Olá URL usada para implantação de preparo de saudação. Implante seu ambiente de preparo do toohello de serviço de nuvem sem a inclusão de um certificado ou qualquer informação de certificado. Uma vez implantado, você pode determinar Olá baseado em GUID URL, que é listado em Olá portal clássico do Azure **URL do Site** campo. Criar um certificado com hello comuns CN (nome) toohello igual com base em GUID URL (por exemplo, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Use Olá tooadd de portal clássico do Azure Olá certificado tooyour testados serviço de nuvem. Em seguida, adicione Olá certificado informações tooyour CSDEF arquivos e CSCFG, reempacotar seu aplicativo e atualizar sua implantação de preparo toouse Olá novo pacote de.

## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
