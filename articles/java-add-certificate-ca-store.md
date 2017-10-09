---
title: "aaaAdd um repositório de autoridade de certificação de Java toohello certificados | Microsoft Docs"
description: "Saiba como tooadd um certificado de CA de Java toohello (cacerts) do certificado de autoridade de certificado armazenar para serviço Twilio ou barramento de serviço do Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Adicionando um certificado toohello repositório de certificados de autoridade de certificação de Java
Olá, as etapas a seguir mostra como tooadd um certificado de CA de Java toohello (cacerts) do certificado de autoridade de certificado armazenados. exemplo Hello usado para o certificado de autoridade de certificação de saudação precisa Olá serviço Twilio. As informações fornecidas posteriormente no tópico Olá descrevem como tooinstall Olá autoridade de certificação do certificado para hello Azure Service Bus. 

Você pode usar keytool tooadd Olá Canadá certificado anterior toozipping seu JDK e adicioná-lo tooyour projeto do Azure **approot** pasta, ou você pode executar uma tarefa de inicialização do Azure que usa keytool tooadd Olá certificado. Este exemplo presume que você adicionará uma autoridade de certificação certificado anterior toohello JDK sendo compactado. Além disso, um certificado de autoridade de certificação específico será usado no exemplo hello, mas as etapas de saudação de obter um certificado de autoridade de certificação diferente e importá-los para Olá cacerts repositório seriam semelhante.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>tooadd cacerts de toohello um certificado armazenar
1. No prompt de comando que é definido do JDK tooyour **jdk\jre\lib\security** pasta, execute Olá toosee quais certificados são instalados a seguir:
   
    `keytool -list -keystore cacerts`
   
    Você será solicitado a fornecer senha de saudação do repositório. a senha padrão Olá é **changeit**. (Se desejar que a senha de saudação toochange, consulte a documentação de keytool Olá em <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) Este exemplo pressupõe um certificado com impressão digital de MD5 67:CB:9 D Olá: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 não estiver listada, e que você deseja tooimport it (esse certificado específico é necessário por Olá serviço Twilio API).
2. Obter certificado de saudação de lista de saudação de certificados listados em [certificados de raiz GeoTrust](http://www.geotrust.com/resources/root-certificates/). Clique o link Olá certificado Olá com número de série 35:DE:F4:CF e salvá-lo toohello **jdk\jre\lib\security** pasta. Para fins deste exemplo, que foi salvo o arquivo tooa chamado **Equifax\_seguro\_certificado\_Authority.cer**.
3. Importar o certificado de saudação via Olá comando a seguir:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Quando solicitado tootrust esse certificado, se o certificado de saudação tiver 67:CB:9 de impressão digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, responder digitando **y**.
4. Olá execução após o certificado de autoridade de certificação de saudação tooensure comando foi importado com êxito:
   
    `keytool -list -keystore cacerts`
5. Compacte Olá JDK e adicioná-lo tooyour projeto do Azure **approot** pasta.

Para obter mais informações sobre o keytool, consulte <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certificados de Raiz do Azure
Os aplicativos que usam os serviços do Azure (por exemplo, o barramento de serviço do Azure) necessitam certificado do tootrust Olá Baltimore CyberTrust Root. (Começando em 15 de abril de 2013, Azure começou a migrar de saudação GTE CyberTrust Root Global toohello Baltimore CyberTrust Root. Essa migração levou toocomplete de vários meses).

Olá Baltimore certificado pode já estar instalado no seu armazenamento cacerts, portanto Lembre-se Olá toorun **keytool-lista** comando toosee primeiro se ele já existe.

Se você precisar tooadd Olá Baltimore CyberTrust Root, ele tem 02:00:00:b9 do número de série e c de d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 de impressão digital SHA1: 78:db:28:52:ca:e4:74. Ele pode ser baixado de <https://cacert.omniroot.com/bc2025.crt>, salvo o arquivo local tooa com extensão **. cer**e, em seguida, importado usando **keytool** como mostrado acima.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre certificados de raiz Olá usado pelo Azure, consulte [migração de certificado raiz do Azure](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Para saber mais sobre Java, veja [Centro de desenvolvedores do Java](/java/azure).

