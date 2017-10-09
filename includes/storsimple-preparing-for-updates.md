<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="3c719-101">Preparar para atualizações</span><span class="sxs-lookup"><span data-stu-id="3c719-101">Preparing for updates</span></span>
<span data-ttu-id="3c719-102">Você precisará Olá tooperform as etapas a seguir antes de verificar e aplicar a atualização hello:</span><span class="sxs-lookup"><span data-stu-id="3c719-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="3c719-103">Pegue um instantâneo de dados de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c719-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="3c719-104">Certifique-se de que seu controlador de IPs fixo sejam roteável e podem se conectar a toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="3c719-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="3c719-105">IPs fixos serão usados tooservice dispositivo de tooyour de atualizações.</span><span class="sxs-lookup"><span data-stu-id="3c719-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="3c719-106">Você pode testar isso executando Olá seguir cmdlet em cada controlador de interface do Windows PowerShell de saudação do dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="3c719-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="3c719-107">**Saída de exemplo para teste de Conexão quando IPs fixos podem se conectar a toohello da Internet**</span><span class="sxs-lookup"><span data-stu-id="3c719-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

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

<span data-ttu-id="3c719-108">Depois que você concluiu com êxito essas pré-verificações de manuais, você pode continuar tooscan e instalar atualizações de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c719-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

