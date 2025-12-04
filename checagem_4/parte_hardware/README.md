# Parte de hardware: Montagem do minigame da cobrinha


Considere o diagrama de montagem abaixo, contendo:

* Arduino Uno
* Display OLED SSD1306 (I2C)
* Dois botões (controle de rotação da cobra)
* Buzzer piezo
* Resistor de 1 kΩ em série com o buzzer

Seu objetivo será montar esse sistema no Wokwi e implementar, passo a passo, o jogo Snake simplificado.

A seguir estão os requisitos organizados em subtarefas. Todas devem ser realizadas para concluir a questão.

---

## Parte 1 — Montagem do hardware no Wokwi

Monte o circuito exatamente conforme as instruções abaixo:

### 1. Display OLED (SSD1306)

Conecte:

* SDA → A4
* SCL → A5
* VCC → 5V
* GND → GND

### 2. Botão de rotação para a direita

Conecte:

* Terminal do botão → pino 2
* Outro terminal → GND
* Utilize `INPUT_PULLUP` no software

### 3. Botão de rotação para a esquerda

Conecte:

* Terminal do botão → pino 3
* Outro terminal → GND
* Utilize `INPUT_PULLUP` no software

### 4. Buzzer com resistor

Conecte:

* Pino 11 → resistor de 1 kΩ → buzzer (terminal positivo)
* Outro terminal do buzzer → GND

---

## Parte 2 — Inicialização do sistema

Implemente no código:

1. Inicialização do OLED usando a biblioteca `Adafruit_SSD1306`.
2. Configuração dos botões como `INPUT_PULLUP`.
3. Configuração do buzzer como `OUTPUT`.
4. Limpeza inicial da tela.

*Dica:*

```cpp
display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
pinMode(2, INPUT_PULLUP);
pinMode(3, INPUT_PULLUP);
pinMode(11, OUTPUT);
display.clearDisplay();
display.display();
```

---

## Parte 3 — Estrutura da cobra

Implemente:

1. Vetores `snakeX[]`, `snakeY[]`.
2. Variável `snakeLength`.
3. Inicialização da cobra com 5 segmentos.
4. Cabeça iniciando no centro da tela.

*Trecho de referência:*

```cpp
snakeX[0] = 64;
snakeY[0] = 32;

for (int i = 1; i < snakeLength; i++) {
    /* completar */
}
```

---

## Parte 4 — Função de rotação com dois botões

Implemente:

1. Uma variável `direction` contendo:
   `0 = UP`, `1 = RIGHT`, `2 = DOWN`, `3 = LEFT`
2. Função `rotateRight()` que soma +1 módulo 4
3. Função `rotateLeft()` que soma +3 módulo 4
4. Leitura dos botões no `loop()` para ajustar a direção

*Trecho de referência:*

```cpp
if (digitalRead(2) == LOW) rotateRight();
if (digitalRead(3) == LOW) rotateLeft();
```

---

## Parte 5 — Movimento da cobra

Implemente a função `moveSnake()`, que deve:

1. Deslocar todos os segmentos seguindo o anterior.
2. Mover a cabeça na direção atual.
3. Implementar teletransporte nas bordas (wrap-around).

*Exemplo de lógica:*

```cpp
if (direction == 0) snakeY[0] -= 4;
if (direction == 1) snakeX[0] += 4;
if (direction == 2) snakeY[0] += 4;
if (direction == 3) snakeX[0] -= 4;
```

---

## Parte 6 — Desenho da tela

Implemente a função `drawSnake()`:

1. Limpar a tela.
2. Desenhar cada segmento com `fillRect(...)`.
3. Desenhar a comida.
4. Atualizar a tela com `display.display()`.

---

## Parte 7 — Sistema de comida e crescimento

Implemente:

1. Função `placeFood()` utilizando coordenadas múltiplas de 4.
2. Detecção de colisão da cabeça com a comida.
3. Aumento de tamanho `snakeLength++`.
4. Novo alimento gerado.
5. Toque sonoro no buzzer.

---

## Parte 8 — Som ao comer

Implemente a função `playEatSound()` com duas notas curtas:

*Exemplo:*

```cpp
tone(11, 900, 60);
delay(70);
tone(11, 1300, 60);
```

---

## Parte 9 — Saída esperada do programa

Ao concluir todas as etapas, o programa deverá apresentar:

1. Uma cobra visível composta por retângulos 4×4.
2. Controles funcionais que giram a cobra:

   * Botão no pino 2: gira 90 graus para a direita
   * Botão no pino 3: gira 90 graus para a esquerda
3. Movimento contínuo com wrap-around nas bordas.
4. Comida aparecendo em posições aleatórias.
5. Tamanho da cobra aumentando ao comer.
6. Buzzer tocando um som curto ao comer.


