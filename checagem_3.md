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



---



Modifique o tempo em que cada luz permanece acesa para criar um ciclo mais rápido ou mais lento.
Você alterar apenas os valores dos `delay()` para experimentar diferentes ritmos do semáforo.

---



Altere o código para que o ciclo comece com o **Semáforo 2** abrindo primeiro, e só depois o Semáforo 1.
A lógica deve manter o funcionamento correto, mas invertendo a ordem dos dois conjuntos.

---



Crie uma fase adicional chamada “atenção piscante”: antes de reiniciar o ciclo, faça **todos os amarelos piscarem 3 vezes**.
Você deve implementar um pequeno laço de repetição para piscar os LEDs amarelos juntos.

---



Reorganize o código de forma que os dados das luzes (quais pinos correspondem a vermelho, amarelo e verde) fiquem agrupados em uma estrutura lógica única, permitindo controlar cada semáforo acessando conjuntos de informações relacionados.
Você deve criar um agrupamento (como um bloco ou conjunto organizado), e ajustar o código para usar essa nova organização.

---



Faça o sistema percorrer automaticamente uma sequência de estados do semáforo armazenada em um conjunto ordenado de passos. Cada passo deve indicar qual cor fica acesa em cada semáforo e por quanto tempo, e o código deve seguir essa sequência repetidamente.
Você deve criar uma lista/coleção de estados, percorrê-la e acionar os LEDs com base nos valores dessa coleção — sem mencionar diretamente o nome da estrutura de dados.




---

# **Entrega**

Você deverá enviar:

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
