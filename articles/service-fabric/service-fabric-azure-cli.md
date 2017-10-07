---
title: "Introdução ao Azure Service Fabric XPlat CLI de aaaGetting"
description: "Introdução à CLI XPlat do Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Usando Olá XPlat CLI toointeract com um cluster do Service Fabric

Você pode interagir com o cluster do Service Fabric máquinas Linux usando Olá XPlat CLI no Linux.

primeira etapa de saudação é obter última versão Olá Olá CLI do representante de git hello e defina-o no seu caminho usando Olá comandos a seguir:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Para cada comando, ele oferece suporte, você pode digitar o nome de saudação de ajuda de Olá Olá comando tooobtain para esse comando.
AutoCompletar tem suporte para comandos de saudação. Por exemplo, hello fornece comando Ajuda para todos os comandos de aplicativo hello a seguir. 

```sh
 azure servicefabric application 
```

Você pode filtrar Olá ajuda tooa comando específico como Olá mostrado no exemplo a seguir:

```sh
 azure servicefabric application  create
```

tooenable preenchimento automático no hello CLI, execute Olá comandos a seguir:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Olá comandos a seguir se conectar a cluster toohello e mostrar Olá nós no cluster de saudação:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse parâmetros nomeados e localizar o que são, você pode digitar – ajuda após um comando. Por exemplo:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Ao conectar-se o cluster de vários computadores tooa de uma máquina **que não faça parte de cluster Olá**, use Olá comando a seguir:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Substitua marca de PublicIPorFQDN Olá com IP real hello ou FQDN conforme apropriado. Ao conectar-se o cluster de vários computadores tooa de uma máquina **que faz parte do cluster Olá**, use Olá comando a seguir:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Você pode usar o PowerShell ou CLI toointeract com o Cluster de malha do serviço de Linux criadas por meio de saudação portal do Azure.

> [!WARNING]
> Esses agrupamentos não são seguros, assim, você pode abrir a caixa de um adicionando o endereço IP público de saudação no manifesto do cluster hello.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Usando Olá cluster do Service Fabric do XPlat CLI tooconnect tooa

Olá comandos de CLI do Azure a seguir descreve como tooconnect tooa proteger o cluster. detalhes do certificado Olá devem corresponder a um certificado em nós de cluster de saudação.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Se seu certificado tem autoridades de certificação (CAs), será necessário tooadd Olá - AC-cert-path parâmetro, como Olá exemplo a seguir: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Se você tiver várias autoridades de certificação, use uma vírgula como delimitador hello.

Se seu nome comum no certificado de saudação não coincide com o ponto de extremidade de conexão de saudação, você pode usar o parâmetro hello `--strict-ssl-false` toobypass Olá verificação, conforme mostrado no hello comando a seguir:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Se você quiser tooskip verificação de saudação da autoridade de certificação, você pode adicionar hello – parâmetro false não autorizado rejeitar conforme mostrado no comando a seguir de saudação: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Depois de se conectar, você deve ser capaz de toorun outros toointeract de comandos CLI com cluster hello.

## <a name="deploying-your-service-fabric-application"></a>Implantando o aplicativo da Malha do Serviço

Execute Olá comandos toocopy, registrar e iniciar o aplicativo de malha do serviço hello a seguir:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Atualizando seu aplicativo

processo de saudação é semelhante toohello [processo no Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Crie, copie, registre e crie seu aplicativo por meio de um diretório raiz do projeto. Se a instância do aplicativo é denominada `fabric:/MySFApp`e o tipo de saudação é MySFApp, comandos Olá seria o seguinte:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Tornar Olá tooyour aplicação de alterações e recriar o serviço Olá modificado.  Saudação de atualização modificada arquivo de manifesto do serviço (ServiceManifest.xml) com as versões atualizada de saudação para Olá serviço (e código ou configuração de dados conforme apropriado). Também modificar o manifesto do aplicativo hello (ApplicationManifest.xml) com número de versão de hello atualizado para o aplicativo hello e Olá serviço modificado.  Agora, copiar e registrar seu aplicativo atualizado usando Olá comandos a seguir:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Agora, você pode iniciar a atualização do aplicativo hello com hello comando a seguir:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Agora você pode monitorar a atualização do aplicativo hello usando SFX. Em alguns minutos, aplicativo hello seria foram atualizado. Também pode tentar um aplicativo atualizado com um erro e verifique a funcionalidade de reversão automática Olá na malha do serviço.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Convertendo do PFX tooPEM e vice-versa

Talvez seja necessário um certificado de tooinstall dos clusters segura de tooaccess do computador local (com o Windows ou Linux) pode estar em um ambiente diferente. Por exemplo, ao acessar um cluster Linux protegido de um computador Windows e vice-versa talvez seja necessário tooconvert seu certificado de PFX tooPEM e vice-versa. 

tooconvert de um PEM tooa arquivo PFX, use Olá comando a seguir:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert de um arquivo PEM de tooa do arquivo PFX, use Olá comando a seguir:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Consulte também[OpenSSL documentação](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para obter detalhes.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Solucionar problemas


### <a name="copying-of-hello-application-package-does-not-succeed"></a>A cópia do pacote de aplicativo hello não for bem-sucedida

Verifique se `openssh` está instalado. Por padrão, a área de trabalho do Ubuntu não está instalada. Instale-o usando Olá comando a seguir:

```sh
sudo apt-get install openssh-server openssh-client**
```

Se Olá problema persistir, tente desabilitar PAM para ssh alterando Olá `sshd_config` arquivo usando Olá comandos a seguir:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Se Olá problema ainda persistir, tente número crescente de saudação do ssh sessões executando Olá comandos a seguir:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Usando chaves de ssh autenticação (como toopasswords contrário) ainda não tem suporte (como plataforma Olá usa ssh pacotes toocopy), para usar a autenticação de senha.

## <a name="next-steps"></a>Próximas etapas

[Configurar o ambiente de desenvolvimento hello e implantar um cluster do Service Fabric application tooa Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Artigos relacionados

* [Introdução ao Service Fabric e à CLI 2.0 do Azure](service-fabric-azure-cli-2-0.md)
