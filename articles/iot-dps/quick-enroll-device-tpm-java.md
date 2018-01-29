---
title: "Registrar o dispositivo TPM no Serviço de Provisionamento de Dispositivos do Azure usando Java | Microsoft Docs"
description: "Guia de Início Rápido do Azure – Registrar dispositivo TPM no Serviço de Provisionamento de Dispositivos do Hub IoT usando o SDK do serviço Java"
services: iot-dps
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 12/20/2017
ms.topic: hero-article
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: f57b5304b8dc575d157f970312e71463496bf10d
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-java-service-sdk"></a>Registrar dispositivo TPM no Serviço de Provisionamento de Dispositivos do Hub IoT usando o SDK do serviço Java
> [!div class="op_single_selector"]
> * [Java](quick-enroll-device-tpm-java.md)
> * [Node.js](quick-enroll-device-tpm-node.md)

Estas etapas mostram como registrar um dispositivo TPM simulado programaticamente nos Serviços de Provisionamento de Dispositivos do Hub IoT do Azure usando o [SDK do serviço Java](https://azure.github.io/azure-iot-sdk-java/service/) com a ajuda de um aplicativo Java de exemplo. Embora o SDK do serviço Java funcione em computadores Windows e Linux, este artigo usa um computador de desenvolvimento do Windows para percorrer o processo de registro.

Certifique-se de [configurar o Serviço de Provisionamento de Dispositivos do Hub IoT com o Portal do Azure](./quick-setup-auto-provision.md), além de [simular um dispositivo TPM](quick-create-simulated-device.md#simulatetpm) antes de continuar.

<a id="setupdevbox"></a>

## <a name="prepare-the-development-environment"></a>Preparar o ambiente de desenvolvimento 

1. Certifique-se de ter o [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalado no computador. 

2. Configure variáveis de ambiente para a instalação do Java. A variável `PATH` deve incluir o caminho completo para o diretório *jdk1.8.x\bin*. Se for a primeira instalação do Java do seu computador, crie uma nova variável de ambiente chamada `JAVA_HOME` e aponte-a para o caminho completo para o diretório *jdk1.8.x*. No computador Windows, geralmente este diretório está localizado na pasta *C:\\Arquivos de Programas\\Java\\* e é possível criar ou editar variáveis de ambiente pesquisando **Editar as variáveis de ambiente do sistema** no **Painel de Controle** do seu computador Windows. 

  Verifique se o Java foi instalado com sucesso em seu computador executando o seguinte comando na janela de comando:

    ```cmd\sh
    java -version
    ```

3. Baixe e extraia [Maven 3](https://maven.apache.org/download.cgi) em seu computador. 

4. Edite a variável de ambiente `PATH` para apontar para a pasta *apache-maven-3.x.x\\bin* dentro da pasta para a qual o Maven foi extraído. Você pode confirmar que o Maven foi instalado com sucesso executando este comando em sua janela de comando:

    ```cmd\sh
    mvn --version
    ```

5. Verifique se o [git](https://git-scm.com/download/) está instalado em seu computador e se foi adicionado à variável de ambiente `PATH`. 


<a id="javasample"></a>

## <a name="download-and-modify-the-java-sample-code"></a>Baixar e modificar o código de exemplo do Java

Esta seção mostra como adicionar os detalhes de provisionamento do dispositivo TPM ao código de exemplo. 

1. Abra um prompt de comando. Clone o repositório do GitHub para o exemplo de código de registro do dispositivo usando o SDK do serviço Java:
    
    ```cmd\sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

2. No código-fonte baixado, navegue até a pasta de exemplo **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**. Abra o arquivo **_/src/main/java/samples/com/microsoft/azure/sdk/iot/ServiceEnrollmentSample.java_** em um editor de sua escolha e adicione os seguintes detalhes:

    1. Adicione o `[Provisioning Connection String]` do serviço de provisionamento do portal desta forma:
        1. Navegue até seu serviço de provisionamento no [Portal do Azure](https://portal.azure.com). 
        2. Abra s **Políticas de acesso compartilhadas** e selecione uma política que tem a permissão *EnrollmentWrite*.
        3. Copie a **Cadeia de conexão da chave primária**. 

            ![Obter a cadeia de conexão de provisionamento do portal](./media/quick-enroll-device-tpm-java/provisioning-string.png)  

        4. No arquivo de código de exemplo **_ServiceEnrollmentSample.java_**, substitua o `[Provisioning Connection String]` por uma **cadeia de conexão de chave primária**.
    
            ```Java
            private static final String PROVISIONING_CONNECTION_STRING = "[Provisioning Connection String]";
            ```

    2. Adicione os detalhes do dispositivo TPM:
        1. Obtenha a *ID de registro* e a *chave de endosso do TPM* para uma simulação de dispositivo TPM, seguindo as etapas que levam à seção [Simular dispositivo TPM](quick-create-simulated-device.md#simulatetpm).
        2. Use a **_ID de Registro_** e a **_Chave de Endosso_** da saída da etapa anterior para substituir o `[RegistrationId]` e `[TPM Endorsement Key]` no arquivo de código de exemplo **_ServiceEnrollmentSample.java_**:
        
            ```Java
            private static final String REGISTRATION_ID = "[RegistrationId]";
            private static final String TPM_ENDORSEMENT_KEY = "[TPM Endorsement Key]";
            ```

    3. Opcionalmente, você pode configurar seu serviço de provisionamento por meio do código de exemplo:
        - Para adicionar essa configuração ao exemplo, siga estas etapas:
            1. Navegue até o hub IoT vinculado ao serviço de provisionamento no [Portal do Azure](https://portal.azure.com). Abra a guia **Visão geral** do hub e copie o **Nome do host**. Atribua este **Nome do host** ao parâmetro *IOTHUB_HOST_NAME*.
                ```Java
                private static final String IOTHUB_HOST_NAME = "[Host name].azure-devices.net";
                ```
            2. Atribua um nome amigável ao parâmetro *DEVICE_ID* e mantenha o *PROVISIONING_STATUS* como o valor padrão *ENABLED*. 
    
        - OU, se você optar por não configurar o serviço de provisionamento, certifique-se de comentar ou excluir as seguintes instruções no arquivo _ServiceEnrollmentSample.java_:
            ```Java
            // The following parameters are optional. Remove it if you don't need.
            individualEnrollment.setDeviceId(DEVICE_ID);
            individualEnrollment.setIotHubHostName(IOTHUB_HOST_NAME);
            individualEnrollment.setProvisioningStatus(PROVISIONING_STATUS);
            ```

    4. Estude o exemplo de código. Ele cria, atualiza, consulta e exclui um registro de dispositivo TPM individual. Para verificar o registro bem-sucedido no portal, comente temporariamente as seguintes linhas de código no fim do arquivo _ServiceEnrollmentSample.java_:
    
        ```Java
        // *********************************** Delete info of individualEnrollment ************************************
        System.out.println("\nDelete the individualEnrollment...");
        provisioningServiceClient.deleteIndividualEnrollment(REGISTRATION_ID);
        ```

    5. Salve o arquivo _ServiceEnrollmentSample.java_.

<a id="runjavasample"></a>

## <a name="build-and-run-the-java-sample-code"></a>Compilar e executar o código de exemplo do Java

1. Abra uma janela de comando e navegue até a pasta **_azure-iot-sdk-java/provisioning/provisioning-samples/service-enrollment-sample_**.

2. Compile o código de exemplo usando este comando:

    ```cmd\sh
    mvn install -DskipTests
    ```

   Esse comando baixa o pacote do Maven [`com.microsoft.azure.sdk.iot.provisioning.service`](https://www.mvnrepository.com/artifact/com.microsoft.azure.sdk.iot.provisioning/provisioning-service-client) para o seu computador. Esse pacote inclui os binários do SDK do serviço Java, de que o código de exemplo precisa para compilar. 

3. Execute o exemplo usando estes comandos na janela de comando:

    ```cmd\sh
    cd target
    java -jar ./service-enrollment-sample-{version}-with-deps.jar
    ```

4. Observe se o registro foi bem-sucedido na janela de saída. 

5. Navegue até seu serviço de provisionamento no Portal do Azure. Clique em **Gerenciar registros** e selecione a guia **Registros individuais**. Observe que a *ID de registro* do dispositivo TPM simulado agora está listada. 

    ![Verifique o registro TPM bem-sucedido no portal](./media/quick-enroll-device-tpm-java/verify-tpm-enrollment.png)  

## <a name="clean-up-resources"></a>Limpar recursos
Se você planeja explorar o exemplo do serviço Java, não limpe os recursos criados neste guia de início rápido. Caso contrário, use as etapas a seguir para excluir todos os recursos criados por este Guia de Início Rápido.

1. Feche a janela de saída de exemplo do Java no computador.
1. Feche a janela do simulador TPM que você talvez tenha criado para simular seu dispositivo TPM.
1. Navegue até o serviço de provisionamento do dispositivo no Portal do Azure, clique em **Gerenciar registros** e, em seguida, selecione a guia **Registros individuais**. Selecione a *ID de Registro* do dispositivo registrado usando este Guia de Início Rápido e clique no botão **Excluir** na parte superior da folha. 

## <a name="next-steps"></a>Próximas etapas
Neste guia de início rápido, você registrou um dispositivo TPM simulado para seu serviço de provisionamento de dispositivos. Para saber mais sobre os detalhes de configuração do dispositivo, prossiga para o tutorial de configuração do Serviço de Provisionamento de Dispositivos no portal do Azure. 

> [!div class="nextstepaction"]
> [Tutoriais do Serviço de Provisionamento de Dispositivos no Hub IoT do Azure](./tutorial-set-up-cloud.md)
