# Checagem 4: Snake no Arduino + OLED SSD1306

Neste projeto, você irá implementar, passo a passo, uma versão da clássica Snake, utilizando:

* Arduino Uno
* Display OLED 128×64 (SSD1306)
* Dois botões (girar a cobra)
* Um buzzer (som ao comer)

---

# TAREFA 1 — Configuração básica do display e hardware

### Objetivo

Configurar o OLED, botões e buzzer.

### Itens para implementar

1. Inicializar o display OLED (`Adafruit_SSD1306`).
2. Configurar botões com `INPUT_PULLUP`.
3. Configurar buzzer com `OUTPUT`.
4. Limpar o display no início.

### Dica de código

```cpp
if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    for(;;); // travar se der erro
}

pinMode(BOTAO_DIREITA, INPUT_PULLUP);
pinMode(BOTAO_ESQUERDA, INPUT_PULLUP);
pinMode(BUZZER, OUTPUT);

display.clearDisplay();
display.display();
```

### Saída esperada

* OLED inicializa e acende.
* Tela preta e limpa.
* Nenhum erro no Monitor Serial.

---

# TAREFA 2 — Criar a cobra inicial

### Objetivo

Criar o vetor de coordenadas que representa o corpo da Snake.

### Itens para implementar

1. Declarar `snakeX[]`, `snakeY[]` e `snakeLength`.
2. Colocar a cabeça no centro.
3. Criar 4 segmentos atrás dela (cobra inicial com tamanho 5).

### Esqueleto de código

```cpp
int snakeX[100];
int snakeY[100];
int snakeLength = 5;

void initSnake() {
    int startX = 64;
    int startY = 32;

    snakeX[0] = startX;
    snakeY[0] = startY;

    for (int i = 1; i < snakeLength; i++) {
        // preencha aqui:
        // snakeX[i] = ???
        // snakeY[i] = ???
    }
}
```

### Saída esperada

* A cabeça deve começar no centro da tela.
* Seguintes segmentos devem aparecer alinhados atrás dela.

---

# TAREFA 3 — Gerar comida aleatória

### Objetivo

Criar a função `placeFood()`.

### Dicas

* Use valores múltiplos de 4 para alinhar o grid.
* Exemplo:

```cpp
foodX = random(0, 128/4) * 4;
foodY = random(0, 64/4) * 4;
```

### Esqueleto

```cpp
void placeFood() {
    // implemente aqui
}
```

### Saída esperada

* Comida aparece como um pequeno quadrado no display.
* Sempre dentro da tela.

---

# TAREFA 4 — Rotação da snake

### Objetivo

Controlar a direção com dois botões:

* Um gira 90° para a direita
* Outro gira 90° para a esquerda

### Direções

```
0 = UP
1 = RIGHT
2 = DOWN
3 = LEFT
```

### Fórmulas

* Girar para a direita:

  ```cpp
  direction = (direction + 1) % 4;
  ```
* Girar para a esquerda:

  ```cpp
  direction = (direction + 3) % 4;
  ```

### Esqueleto

```cpp
if (digitalRead(BOTAO_DIREITA) == LOW) {
    rotateRight();
}

if (digitalRead(BOTAO_ESQUERDA) == LOW) {
    rotateLeft();
}
```

### Saída esperada

* Cobra gira instantaneamente 90° ao apertar os botões.

---

# TAREFA 5 — Movimento da cobra

### Objetivo

Mover a cobra pela tela.

### Itens para implementar

1. Cada segmento deve assumir a posição do anterior.
2. A cabeça deve se mover conforme a direção.
3. Implementar "wrap-around": sair pela direita volta pela esquerda etc.

### Esqueleto

```cpp
void moveSnake() {

    for (int i = snakeLength - 1; i > 0; i--) {
        snakeX[i] = snakeX[i - 1];
        snakeY[i] = snakeY[i - 1];
    }

    if (direction == 0) snakeY[0] -= 4;
    if (direction == 1) snakeX[0] += 4;
    if (direction == 2) snakeY[0] += 4;
    if (direction == 3) snakeX[0] -= 4;

    // wrap-around
    // implemente aqui
}
```

### Saída esperada

* Cobra se move suavemente.
* Não trava ao chegar nas bordas.

---

# TAREFA 6 — Desenhar a cobra

### Objetivo

Mostrar a cobra e a comida no display.

### Esqueleto

```cpp
void drawSnake() {
    display.clearDisplay();

    // comida
    display.fillRect(foodX, foodY, 4, 4, WHITE);

    // corpo da snake
    for (int i = 0; i < snakeLength; i++) {
        display.fillRect(snakeX[i], snakeY[i], 4, 4, WHITE);
    }

    display.display();
}
```

### Saída esperada

* Corpo inteiro aparece no OLED.
* Comida aparece corretamente.

---

# TAREFA 7 — Comer e crescer

### Objetivo

Implementar crescimento ao comer.

### Itens para implementar

1. Detectar colisão da cabeça com a comida.
2. Aumentar `snakeLength`.
3. Gerar nova comida.
4. Tocar som com `playEatSound()`.

### Esqueleto

```cpp
if (snakeX[0] == foodX && snakeY[0] == foodY) {
    snakeLength++;
    playEatSound();
    placeFood();
}
```

### Saída esperada

* Cobra aumenta de tamanho.
* Novo alimento aparece.
* Som toca corretamente.

---

# TAREFA 8 — Som ao comer (buzzer)

### Objetivo

Criar feedback sonoro ao comer.

### Esqueleto

```cpp
void playEatSound() {
    tone(BUZZER, 800, 80);
    delay(50);
    tone(BUZZER, 1200, 80);
}
```

### Saída esperada

* Um som curto toca sempre que a cobra come.

---

# OPCIONAL — TAREFA 9 — Colisão com o próprio corpo

### Objetivo

Finalizar o jogo ao colidir com o próprio corpo.

### Esqueleto

```cpp
bool checkSelfCollision() {
    for (int i = 1; i < snakeLength; i++) {
        if (snakeX[0] == snakeX[i] && snakeY[0] == snakeY[i]) {
            return true;
        }
    }
    return false;
}
```

No loop principal:

```cpp
if (checkSelfCollision()) {
    gameOver();
}
```

### Saída esperada

* Tela exibe "GAME OVER" ao bater no corpo.

---

# OPCIONAL — TAREFA 10 — Velocidade aumenta conforme cresce

### Objetivo

Aumentar dificuldade automaticamente à medida que a cobra cresce.

### Dica

```cpp
speedDelay = 120 - snakeLength;
if (speedDelay < 40) speedDelay = 40;
```

### Saída esperada

* Conforme a cobra aumenta, a velocidade do jogo também aumenta.


