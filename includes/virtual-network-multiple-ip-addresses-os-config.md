## <a name="os-config"></a>Adicionar sistema operacional do IP endereços tooa VM

Conecte-se e logon tooa VM que você criou com vários endereços IP privados. Você deve adicionar manualmente todos os Olá endereços IP privados (incluindo Olá primário) que você adicionou toohello VM. Olá completo seguindo as etapas para seu sistema operacional VM:

### <a name="windows"></a>Windows

1. Em um prompt de comando, digite *ipconfig /all*.  Você só verá Olá *primário* endereço IP privado (por meio de DHCP).
2. Tipo *ncpa.cpl* no prompt de comando de Olá tooopen Olá **conexões de rede** janela.
3. Abrir as propriedades de saudação do adaptador apropriado Olá: **Conexão de área Local**.
4. Clique duas vezes em versão do Protocolo de Internet 4 (IPv4).
5. Selecione **Olá Use seguinte endereço IP** e digite Olá valores a seguir:

    * **Endereço IP**: insira Olá *primário* endereço IP privado
    * **Máscara de sub-rede**: defina com base na sua sub-rede. Por exemplo, se hello sub-rede é um /24 subrede e sub-rede Olá máscara é 255.255.255.0.
    * **Gateway padrão**: Olá primeiro endereço IP na sub-rede hello. Se sua sub-rede for 10.0.0.0/24, o endereço IP do gateway de saudação é 10.0.0.1.
    * Clique em **Olá usar endereços de servidor DNS a seguir** e digite Olá valores a seguir:
        * **Servidor DNS preferencial**: digite 168.63.129.16 se você não estiver usando seu próprio servidor DNS.  Se você estiver usando seu próprio servidor DNS, digite o endereço IP de saudação do servidor.
    * Clique em Olá **avançado** botão e adicionar mais endereços IP. Adicione cada Olá secundários endereços IP privados listados na etapa 8 toohello NIC com hello mesma sub-rede especificada para o endereço IP primário de saudação.
        >[!WARNING] 
        >Se você não seguir as etapas de saudação acima corretamente, você pode perder conectividade tooyour VM. Certifique-se de que informações Olá inseridas para a etapa 5 são precisas antes de continuar.

    * Clique em **Okey** tooclose configurações Olá TCP/IP e, em seguida, **Okey** novamente tooclose Olá as configurações do adaptador. A conexão RDP é restabelecida.

6. Em um prompt de comando, digite *ipconfig /all*. Todos os endereços IP que você adicionou são mostrados e o DHCP está desativado.


### <a name="validation-windows"></a>Validação (Windows)

tooensure você toohello tooconnect capaz de internet por meio de sua configuração de IP secundária via Olá que IP público associado, depois que ela tiver sido adicionada corretamente usando as etapas acima, use Olá comando a seguir:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para configurações de IP secundárias, você pode apenas executar ping toohello Internet se a configuração de saudação tem um endereço IP público associado a ele. Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello da Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Abra uma janela de terminal.
2. Verifique se que você for usuário de raiz de saudação. Se você não estiver, digite Olá comando a seguir:

    ```bash
    sudo -i
    ```

3. Atualize o arquivo de configuração de Olá Olá da interface de rede (assumindo 'eth0').

    * Lembre-Olá item de linha existente do dhcp. endereço IP primário Olá permanece configurado que era anteriormente.
    * Adicione uma configuração para um endereço IP estático adicional com hello comandos a seguir:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Você deve ver um arquivo. cfg.
4. Arquivo hello aberto. Você deve ver Olá linhas final de saudação do arquivo hello seguintes:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Adicione Olá linhas a seguir depois de linhas de saudação que existem neste arquivo:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Salve arquivo hello usando Olá comando a seguir:

    ```bash
    :wq
    ```

7. Redefinição de interface de rede Olá com hello comando a seguir:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Execute ifdown e ifup em Olá mesmo linha se usando uma conexão remota.
    >

8. Verifique se o endereço IP de saudação é adicionado toohello interface de rede com hello comando a seguir:

    ```bash
    ip addr list eth0
    ```

    Você deve ver Olá IP endereço adicionados como parte da lista de saudação.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS e outros)

1. Abra uma janela de terminal.
2. Verifique se que você for usuário de raiz de saudação. Se você não estiver, digite Olá comando a seguir:

    ```bash
    sudo -i
    ```

3. Digite sua senha e siga as instruções conforme solicitado. Quando você for usuário de raiz Olá, navegue até toohello pasta de scripts de rede com hello comando a seguir:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Ifcfg arquivos usando o comando a seguir de saudação relacionados a saudação da lista:

    ```bash
    ls ifcfg-*
    ```

    Você deve ver *ifcfg eth0* como um dos arquivos de saudação.

5. tooadd um endereço IP, crie um arquivo de configuração para ele, conforme mostrado abaixo. Observe que um arquivo deve ser criado para cada configuração de IP.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Olá abrir *ifcfg-eth0:0* arquivo com hello comando a seguir:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Adicionar arquivo de conteúdo toohello *eth0:0* nesse caso, com hello comando a seguir. Ser tooupdate informações com base no seu endereço IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Salve o arquivo de saudação com hello comando a seguir:

    ```bash
    :wq
    ```

9. Reinicie os serviços de rede hello e certifique-se de alterações de saudação terão êxito executando Olá comandos a seguir:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Você deve ver Olá IP endereço que você adicionou, *eth0:0*, na lista de saudação retornada.

### <a name="validation-linux"></a>Validação (Linux)

tooensure são toohello tooconnect capaz de internet por meio de sua configuração de IP secundária por meio de IP público Olá associá-lo, use Olá comando a seguir:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para configurações de IP secundárias, você pode apenas executar ping toohello Internet se a configuração de saudação tem um endereço IP público associado a ele. Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello da Internet.

Para VMs do Linux, quando você tentar toovalidate conectividade de saída de uma NIC secundário, talvez seja necessário rotas apropriadas tooadd. Há muitos toodo de maneiras isso. Veja a documentação apropriada para sua distribuição do Linux. a seguir Olá este é um tooaccomplish de método:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Ser tooreplace-se de que:
    - **10.0.0.5** com hello privada endereço que tem um IP público endereço IP associado tooit
    - **10.0.0.1** gateway padrão de tooyour
    - **eth2** toohello nome de sua NIC secundário
