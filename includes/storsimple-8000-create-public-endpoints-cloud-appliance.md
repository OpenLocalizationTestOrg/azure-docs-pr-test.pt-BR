#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>pontos de extremidade públicos no dispositivo de nuvem Olá toocreate

1. Entrar toohello portal do Azure.
2. Vá muito**máquinas virtuais**, selecione e clique em máquina virtual Olá que está sendo usada como o dispositivo de nuvem.
    
3. É necessário toocreate um fluxo de saudação rede segurança grupo (NSG) regra toocontrol de tráfego dentro e fora de sua máquina virtual. Execute Olá seguindo as etapas toocreate uma regra NSG.
    1. Selecione **Grupo de segurança de rede**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Clique em saudação padrão grupo de segurança que é apresentado.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Selecione **Regras de segurança de entrada**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Clique em **+ adicionar** toocreate uma regra de segurança de entrada.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Na folha de regra de segurança de entrada do hello adicionar:

        1. Para Olá **nome**, digite o seguinte Olá nome para o ponto de extremidade de saudação: WinRMHttps.
        
        2. Para Olá **prioridade**, selecione um número menor que 1000 (que é a prioridade de saudação de regra padrão de saudação). Valor mais alto do hello, prioridade inferior a saudação.

        3. Saudação de conjunto **fonte** muito**qualquer**.

        4. Para Olá **Service**, selecione **WinRM**. Olá **protocolo** é definida automaticamente muito**TCP** e hello **intervalo de portas** está definido muito**5986**.

        5. Clique em **Okey** toocreate regra de saudação.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. A etapa final é tooassociate ao grupo de segurança da sua rede com uma sub-rede ou uma interface de rede específico. Execute Olá tooassociate as etapas a seguir em seu grupo de segurança de rede com uma sub-rede.
    1. Vá muito**sub-redes**.
    2. Clique em **+ Associar**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Selecione a rede virtual e selecione sub-rede apropriada hello.
    4. Clique em **Okey** toocreate regra de saudação.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Depois Olá regra for criada, você pode exibir seu endereço de IP Virtual público (VIP) detalhes toodetermine hello. Registre esse endereço.


