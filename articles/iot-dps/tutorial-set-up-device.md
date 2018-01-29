---
title: "Configurar o dispositivo para o Serviço de Provisionamento de Dispositivos no Hub IoT do Azure | Microsoft Docs"
description: "Configurar o dispositivo para provisionar por meio do Serviço de Provisionamento de Dispositivos no Hub IoT durante o processo de fabricação do dispositivo"
services: iot-dps
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: 835a54f147b9ea543df21e7dfeb226ac42aceda3
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2017
---
# <a name="set-up-a-device-to-provision-using-the-azure-iot-hub-device-provisioning-service"></a>Configurar um dispositivo para provisionar usando o Serviço de Provisionamento de Dispositivos no Hub IoT do Azure

No tutorial anterior, você aprendeu como configurar o Serviço de Provisionamento de Dispositivos no Hub IoT do Azure para provisionar automaticamente os dispositivos para o Hub IoT. Este tutorial fornece diretrizes para configurar seu dispositivo durante o processo de fabricação, de modo que você possa configurar o Serviço de Provisionamento de Dispositivos para seu dispositivo com base no respectivo [HSM (módulo de segurança de hardware)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security) e o dispositivo possa se conectar ao Serviço de Provisionamento de Dispositivos quando ele for inicializado pela primeira vez. Este tutorial aborda os processos para:

> [!div class="checklist"]
> * Selecionar um módulo de segurança de hardware
> * Compilar o SDK de cliente de provisionamento de dispositivos para o HSM selecionado
> * Extrair os artefatos de segurança
> * Definir a configuração do Serviço de Provisionamento de Dispositivos no dispositivo

## <a name="prerequisites"></a>pré-requisitos

Antes de prosseguir, crie sua instância do Serviço de Provisionamento de Dispositivos e um Hub IoT usando as instruções mencionadas no tutorial [Configurar a nuvem para provisionamento de dispositivos](./tutorial-set-up-cloud.md).


## <a name="select-a-hardware-security-module"></a>Selecionar um módulo de segurança de hardware

O [SDK do cliente do Serviço de Provisionamento de Dispositivos](https://github.com/Azure/azure-iot-sdk-c/tree/master/provisioning_client) dá suporte a dois tipos de módulos de segurança de hardware (ou HSMs): 

- [TPM (Trusted Platform Module)](https://en.wikipedia.org/wiki/Trusted_Platform_Module).
    - O TPM é um padrão estabelecido para a maioria das plataformas de dispositivo baseadas em Windows, bem como alguns dispositivos baseados em Linux/Ubuntu. Como um fabricante de dispositivos, você pode escolher esse HSM se você tem um desses sistemas operacionais em execução em seus dispositivos e se você está procurando um padrão estabelecido para HSMs. Com chips do TPM, você só pode registrar cada dispositivo individualmente para o Serviço de Provisionamento de Dispositivos. Para fins de desenvolvimento, você pode usar o simulador do TPM no seu computador de desenvolvimento do Windows ou Linux.

- Módulos de segurança de hardware baseados em [X.509](https://cryptography.io/en/latest/x509/). 
    - HSMs baseados em X.509 são chips relativamente mais recentes, com trabalho atualmente em andamento na Microsoft para chips RIoT ou DICE que implementam os certificados X.509. Com chips X.509, você pode fazer o registro em massa no portal. Ele também dá suporte a determinados OSes não Windows como embedOS. Para fins de desenvolvimento, o SDK do cliente do Serviço de Provisionamento de Dispositivos dá suporte a um simulador de dispositivo de X.509. 

Como um fabricante de dispositivos, você precisa selecionar chips/módulos de segurança de hardware com base em um dos tipos anteriores. Outros tipos de HSMs atualmente não têm suporte no SDK do cliente do Serviço de Provisionamento de Dispositivos.   


## <a name="build-device-provisioning-client-sdk-for-the-selected-hsm"></a>Compilar o SDK de cliente de provisionamento de dispositivos para o HSM selecionado

O SDK de cliente do Serviço de Provisionamento de Dispositivos ajuda a implementar o mecanismo de segurança selecionado no software. As etapas a seguir mostram como usar o SDK para o chip do HSM selecionado:

1. Se você seguiu o [Guia de início rápido para criar dispositivo simulado](./quick-create-simulated-device.md), você tem a configuração pronta para compilar o SDK. Caso contrário, siga as quatro primeiras etapas da seção intitulada [Preparar o ambiente de desenvolvimento](./quick-create-simulated-device.md#setupdevbox). Essas etapas clonam o repositório GitHub para o SDK do cliente do Serviço de Provisionamento de Dispositivos, bem como instalam a ferramenta de build `cmake`. 

1. Compile o SDK para o tipo de HSM que você selecionou para seu dispositivo, usando um dos seguintes comandos no prompt de comando:
    - Para dispositivos TPM:
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON ..
        ```

    - Para simulador de TPM:
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
        ```

    - Para dispositivos X.509 e simulador:
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON ..
        ```

1. O SDK fornece suporte padrão para dispositivos que executam o implementações Windows ou Ubuntu para HSMs X.509 e TPM. Para esses HSMs com suporte, vá para a seção intitulada [Extrair os artefatos de segurança](#extractsecurity) abaixo. 
 
## <a name="support-custom-tpm-and-x509-devices"></a>Suporte a dispositivos TPM e X.509 personalizados

O SDK do cliente do sistema de provisionamento de dispositivos não dá suporte a nenhum dispositivo TPM e X.509 que não são executam o Windows ou Ubuntu. Para esses dispositivos, você precisa escrever o código personalizado para o chip do HSM específico, conforme mostrado nas etapas a seguir:

### <a name="develop-your-custom-repository"></a>Desenvolver seu repositório personalizado

1. Desenvolver uma biblioteca para acessar seu HSM. Este projeto deve produzir uma biblioteca estática para o SDK de provisionamento de dispositivos consumir.
1. Sua biblioteca deve implementar as funções definidas no arquivo de cabeçalho a seguir: a. Para TPM personalizado, implemente as funções definidas no [Documento HSM personalizado](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-tpm-api).
    b. Para X.509 personalizado, implemente as funções definidas em [Documento HSM personalizado](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-x509-api). 

### <a name="integrate-with-the-device-provisioning-service-client"></a>Integrar com o cliente do Serviço de Provisionamento de Dispositivos

Após a compilação por conta própria bem-sucedida da biblioteca, mova o C-SDK do Hub IoT e crie um vínculo com sua biblioteca:

1. Forneça o repositório GitHub do HSM personalizado, o caminho da biblioteca e o nome dela no comando cmake a seguir:
    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON -Dhsm_custom_lib=<path_and_name_of_library> <PATH_TO_AZURE_IOT_SDK>
    ```
   
1. Abra o SDK no visual studio e compile-o. 

    - O processo de compilação compilará a biblioteca do SDK.
    - O SDK tentará vincular com o HSM personalizado definido no comando cmake.

1. Execute a amostra `\azure-iot-sdk-c\provisioning_client\samples\prov_dev_client_ll_sample\prov_dev_client_ll_sample.c` para verificar se o seu HSM foi implementado corretamente.

<a id="extractsecurity"></a>
## <a name="extract-the-security-artifacts"></a>Extrair os artefatos de segurança

A próxima etapa é extrair os artefatos de segurança para o HSM no seu dispositivo.

1. Para um dispositivo TPM, você precisará descobrir a **chave de endosso** associada a ele do fabricante do chip do TPM. Você pode derivar uma única **ID de registro** para seu dispositivo TPM via hash da chave de endosso. 
2. Para um dispositivo de X.509, você precisará obter os certificados emitidos para seus dispositivos – certificados de entidade final para registros de dispositivos individuais ou então certificados raiz para registros de dispositivos em grupo.

Esses artefatos de segurança são necessários para registrar seus dispositivos no Serviço de Provisionamento de Dispositivos. O serviço de provisionamento, em seguida, aguarda que qualquer um desses dispositivos inicialize e conectar-se com ele em qualquer ponto posterior no tempo. Consulte [Como gerenciar registros de dispositivo](how-to-manage-enrollments.md) para obter informações sobre como usar esses artefatos de segurança para criar registros. 

Quando o dispositivo é inicializado pela primeira vez, o SDK do cliente interage com o chip para extrair os artefatos de segurança do dispositivo e verifica o registro com o Serviço de Provisionamento de Dispositivos. 


## <a name="set-up-the-device-provisioning-service-configuration-on-the-device"></a>Definir a configuração do Serviço de Provisionamento de Dispositivos no dispositivo

A última etapa no processo de fabricação do dispositivo é escrever um aplicativo que usa o SDK do cliente do Serviço de Provisionamento de Dispositivos para registrar o dispositivo com o serviço. Esse SDK fornece as seguintes APIs para seus aplicativos usarem:

```C
// Creates a Provisioning Client for communications with the Device Provisioning Client Service
PROV_DEVICE_LL_HANDLE Prov_Device_LL_Create(const char* uri, const char* scope_id, PROV_DEVICE_TRANSPORT_PROVIDER_FUNCTION protocol)

// Disposes of resources allocated by the provisioning Client.
void Prov_Device_LL_Destroy(PROV_DEVICE_LL_HANDLE handle)

// Asynchronous call initiates the registration of a device.
PROV_DEVICE_RESULT Prov_Device_LL_Register_Device(PROV_DEVICE_LL_HANDLE handle, PROV_DEVICE_CLIENT_REGISTER_DEVICE_CALLBACK register_callback, void* user_context, PROV_DEVICE_CLIENT_REGISTER_STATUS_CALLBACK reg_status_cb, void* status_user_ctext)

// Api to be called by user when work (registering device) can be done
void Prov_Device_LL_DoWork(PROV_DEVICE_LL_HANDLE handle)

// API sets a runtime option identified by parameter optionName to a value pointed to by value
PROV_DEVICE_RESULT Prov_Device_LL_SetOption(PROV_DEVICE_LL_HANDLE handle, const char* optionName, const void* value)
```

Lembre-se de inicializar as variáveis `uri` e `id_scope` conforme mencionado na [seção Simular a primeira sequência de inicialização para o dispositivo deste guia de início rápido](./quick-create-simulated-device.md#firstbootsequence), antes de usá-las. A API `Prov_Device_LL_Create` de registro do cliente de provisionamento de dispositivos conecta-se ao Serviço de Provisionamento de Dispositivos global. O *escopo da ID* é gerado pelo serviço e assegura a exclusividade. É imutável e é usado para identificar exclusivamente as IDs de registro. O `iothub_uri` permite que a API `IoTHubClient_LL_CreateFromDeviceAuth` de registro do cliente do Hub IoT se conecte ao Hub IoT correto. 


Essas APIs ajudam seu dispositivo a conectar-se e registrar-se no Serviço de Provisionamento de Dispositivos quando ele é inicializado, a obter as informações sobre o Hub IoT e então conectar-se a ele. O arquivo `provisioning_client/samples/prov_client_ll_sample/prov_client_ll_sample.c` mostra como usar essas APIs. Em geral, você precisa criar a seguinte estrutura para o registro de cliente:

```C
static const char* global_uri = "global.azure-devices-provisioning.net";
static const char* id_scope = "[ID scope for your provisioning service]";
...
static void register_callback(DPS_RESULT register_result, const char* iothub_uri, const char* device_id, void* context)
{
    USER_DEFINED_INFO* user_info = (USER_DEFINED_INFO *)user_context;
    ...
    user_info. reg_complete = 1;
}
static void registation_status(DPS_REGISTRATION_STATUS reg_status, void* user_context)
{
}
int main()
{
    ...
    SECURE_DEVICE_TYPE hsm_type;
    hsm_type = SECURE_DEVICE_TYPE_TPM;
    //hsm_type = SECURE_DEVICE_TYPE_X509;
    prov_dev_security_init(hsm_type); // initialize your HSM 

    prov_transport = Prov_Device_HTTP_Protocol;
    
    PROV_CLIENT_LL_HANDLE handle = Prov_Device_LL_Create(global_uri, id_scope, prov_transport); // Create your provisioning client

    if (Prov_Client_LL_Register_Device(handle, register_callback, &user_info, register_status, &user_info) == IOTHUB_DPS_OK) {
        do {
        // The register_callback is called when registration is complete or fails
            Prov_Client_LL_DoWork(handle);
        } while (user_info.reg_complete == 0);
    }
    Prov_Client_LL_Destroy(handle); // Clean up the Provisioning client
    ...
    iothub_client = IoTHubClient_LL_CreateFromDeviceAuth(user_info.iothub_uri, user_info.device_id, transport); // Create your IoT hub client and connect to your hub
    ...
}
```

Você pode refinar seu aplicativo de registro de cliente do Serviço de Provisionamento de Dispositivos usando um dispositivo simulado primeiro, usando uma configuração de serviço de teste. Depois que o aplicativo está funcionando no ambiente de teste, você pode compilá-lo para o dispositivo específico e copiar o executável para a imagem do dispositivo. Não inicie o dispositivo ainda, você precisa [registrar o dispositivo no Serviço de Provisionamento de Dispositivos](./tutorial-provision-device-to-hub.md#enrolldevice) antes de iniciá-lo. Consulte as próximas etapas abaixo para aprender esse processo. 

## <a name="clean-up-resources"></a>Limpar recursos

Neste ponto, você pode configurar os serviços de provisionamento do dispositivos e do Hub IoT no portal. Se você quiser abandonar a configuração de provisionamento de dispositivos e/ou atrasar o uso de qualquer um desses serviços, é recomendável desligá-los para evitar incorrer em custos desnecessários.

1. No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e selecione o serviço de Provisionamento de Dispositivos. Na parte superior da folha **Todos os recursos**, clique em **Excluir**.  
1. No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e selecione seu Hub IoT. Na parte superior da folha **Todos os recursos**, clique em **Excluir**.  


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Selecionar um módulo de segurança de hardware
> * Compilar o SDK de cliente de provisionamento de dispositivos para o HSM selecionado
> * Extrair os artefatos de segurança
> * Definir a configuração do Serviço de Provisionamento de Dispositivos no dispositivo

Avance para o próximo tutorial para aprender a provisionar o dispositivo para o Hub IoT registrando-o no Serviço de Provisionamento de Dispositivos no Hub IoT do Azure para provisionamento automático.

> [!div class="nextstepaction"]
> [Provisionar o dispositivo para o Hub IoT](tutorial-provision-device-to-hub.md)

