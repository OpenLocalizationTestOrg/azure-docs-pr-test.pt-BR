<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a>toocable de alimentação do seu dispositivo
> [!NOTE]
> Ambos os compartimentos no seu dispositivo StorSimple incluem PCMs redundantes. Para cada compartimento, Olá PCMs deve ser instalado e conectado toodifferent power fontes tooensure alta disponibilidade.
> 
> 

1. Verifique se Olá interruptores em todos os PCMs de saudação estão na posição do hello OFF.
2. No compartimento principal do hello, conecte-se tooboth cabos de alimentação Olá PCMs. Olá cabos de alimentação são identificados em vermelho na alimentação Olá cabeamento diagrama abaixo.
3. Certifique-se de que Olá dois PCMs no hello compartimento principal usam separado fontes de alimentação.
4. Anexe Olá power cabos toohello power em unidades de distribuição do rack Olá conforme mostrado no diagrama de cabeamento de alimentação hello.
5. Repita as etapas 2 a 4 para Olá compartimento EBOD.
6. Ative o compartimento do EBOD Olá colocando o interruptor de energia Olá em cada toohello na posição ligado PCM.
7. Verifique se que Olá compartimento EBOD está ligado observando que LEDs Olá verde Olá parte posterior do controlador do EBOD Olá estão ligados.
8. Ative o compartimento principal Olá colocando cada comutador toohello na posição ligado PCM.
9. Verifique se sistema Olá em assegurando o controlador do dispositivo Olá que LEDs tem ativado.
10. Certifique-se de que conexão Olá entre o controlador do EBOD hello e controlador do dispositivo Olá está ativa verificando que Olá quatro LEDs próxima toohello porta SAS no controlador do EBOD Olá estão verdes.
    
    > [!IMPORTANT]
    > tooensure alta disponibilidade para seu sistema, recomendamos que siga estritamente toohello mostrado no diagrama a seguir de saudação do esquema de cabeamento de alimentação.
    > 
    > 
    
    ![Cabeamento do dispositivo 4U para alimentação](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    **Cabeamento de energia**
    
    | Rótulo | Descrição |
    |:--- |:--- |
    | 1 |Compartimento principal |
    | 2 |PCM 0 |
    | 3 |PCM 1 |
    | 4 |Controlador 0 |
    | 5 |Controlador 1 |
    | 6 |Controlador 0 do EBOD |
    | 7 |Controlador 1 do EBOD |
    | 8 |Compartimento EBOD |
    | 9 |PDUs |

