# **NF3 – Tópicos em Sistemas de Informação**

## **Atividade Prática – Arduino (Semáforo)**

### Curso de Sistemas de Informação – UniAtenas

**Professor:** Prof. Me. Luis Vinicius
**Tema:** Programação embarcada utilizando Arduino
**Link do projeto**: https://wokwi.com/projects/448811467963038721
---

## **Descrição Geral da Atividade**

Nesta atividade, você irá trabalhar com lógica sequencial, controle digital e manipulação de valores lidos do hardware utilizando Arduino Uno no simulador **Wokwi**.

O código-base controla dois conjuntos de LEDs simulando um cruzamento com semáforos.
Seu objetivo é **modificar e estender esse código**, sem alterar o hardware do projeto, cumprindo os desafios propostos abaixo.

Todas as atividades devem ser realizadas **somente editando o código**.

---

## **Arquivos Disponíveis**

* Código-base do semáforo (`semaforo.ino`)
* Projeto Wokwi configurado para Arduino Uno
* Este documento com o enunciado das atividades

---

# **Atividades**

As atividades estão divididas por nível de dificuldade. O aluno deverá **alterar apenas o código**, sem adicionar ou remover componentes do esquema do simulador.

---



### ** Classificação do valor do sensor**

Modifique o código para que, além de mostrar o valor lido de um potenciômetro, o display exiba uma palavra indicando a faixa do valor:

* `< 300` → **"BAIXO"**
* `300 a 700` → **"MÉDIO"**
* `> 700` → **"ALTO"**

Nenhuma alteração de hardware.

---

### ** Exibição invertida opcional**

Crie uma variável booleana chamada `invertido`.

* Se `invertido == true`:
  Mostrar: **"Valor invertido: 1023 - leitura"**

* Se `invertido == false`:
  Mostrar o valor normal do sensor.

A troca deve ser feita **somente alterando a variável no código**.

---


### ** Armazenamento das últimas leituras**

Armazene as **5 leituras mais recentes** do sensor em um conjunto de posições.
Em seguida, calcule a **média** dessas leituras e exiba no display.

**Dica:** sempre que uma nova leitura chegar, ela deve ocupar a próxima posição.
Ao chegar ao final, volte para a primeira posição.

---

### ** Detecção de variação brusca**

Detecte quando a leitura atual aumenta mais de **100 unidades** em relação à leitura anterior.

Se isso acontecer, mostrar no display:

> **"Pico detectado"**

Guarde a última leitura para comparação na iteração seguinte.

---

### ** Estrutura circular + filtro avançado**

Essa atividade possui duas partes:

---

### **🔹 Parte A — Janela deslizante de 10 valores**

Mantenha um grupo fixo de **10 leituras** do sensor.
Sempre que uma nova leitura entrar, a mais antiga deve sair.

Com base nessas 10 leituras, exibir:

* **Média**
* **Menor valor**
* **Maior valor**

---

### **🔹 Parte B — Armazenamento de valores elevados**

Guarde apenas valores **acima de 900**.

A estrutura deve comportar **até 5 valores**:

* Se ainda houver espaço, apenas adicione.
* Se já houver 5 valores e surgir um novo valor acima de 900:
  **remover o valor mais recente** e colocar o novo no lugar.

Exibir sempre o valor mais recentemente armazenado.

---


---

# **Entrega**

O aluno deverá enviar:

✔ Código `.ino` modificado
✔ Prints do funcionamento no Wokwi
✔ Respostas às perguntas solicitadas (quando houver)

Formato aceito: **ZIP** com toda a pasta do projeto.

---

#  **Observações do Professor**

* Não altere pinos, resistores, LEDs ou conexões.
* Não troque o Arduino Uno.
* Toda a lógica deve ser resolvida **somente via software**.

---

#  **Dúvidas?**

Abra uma *Issue* no repositório ou consulte o professor durante o horário de atendimento.
