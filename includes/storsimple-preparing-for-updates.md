<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Preparar para atualizações
Você precisará Olá tooperform as etapas a seguir antes de verificar e aplicar a atualização hello:

1. Pegue um instantâneo de dados de dispositivo de saudação.
2. Certifique-se de que seu controlador de IPs fixo sejam roteável e podem se conectar a toohello da Internet. IPs fixos serão usados tooservice dispositivo de tooyour de atualizações. Você pode testar isso executando Olá seguir cmdlet em cada controlador de interface do Windows PowerShell de saudação do dispositivo hello:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Saída de exemplo para teste de Conexão quando IPs fixos podem se conectar a toohello da Internet**

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

Depois que você concluiu com êxito essas pré-verificações de manuais, você pode continuar tooscan e instalar atualizações de saudação.

