# 🌱 Irrigador Inteligente com Arduino 🌱

## 📚 Descrição do Projeto

Este projeto visa criar um **irrigador inteligente** utilizando um Arduino, que automatiza o processo de irrigação de plantas com base na umidade do solo. O sistema é composto por diversos componentes eletrônicos que permitem monitorar a umidade do solo e acionar uma bomba d'água quando necessário, otimizando o uso de água e garantindo a saúde das plantas.

## 🛠️ Componentes Utilizados

- **Arduino Uno**: Microcontrolador principal que processa os dados do sensor e controla os atuadores.  

- **Sensor de Umidade do Solo**: Detecta o nível de umidade do solo através da resistência elétrica entre duas sondas.  

- **Módulo Relé**: Controla a bomba d'água, permitindo o controle de dispositivos de maior potência.  

- **Bomba d'Água**: Responsável por bombear água para irrigar o solo.  

- **LEDs (Vermelho, Azul, Verde)**: Indicadores visuais para mostrar o status do solo e da bomba.  

- **Resistores**: Protegem os LEDs, limitando a corrente que passa por eles.  

- **Mangueira de Silicone**: Conduz a água da bomba até o solo.  

  ## 🔧 SLIDE DE APRESENTAÇÃO DO CIRCUITO
https://www.canva.com/design/DAGQkCzHoMc/zFujgyaiiqlsuHBn4vN5tA/edit


## 📜 Código do Projeto

```
/*
   PROJETO: Irrigador Inteligente
   DISCIPLINA: Software em Tempo Real
   UNIVERSIDADE: Universidade Federal do Ceará (UFC), Campus Sobral
   CURSO: Engenharia da Computação
   DATA: 09/2024
*/

// Variáveis para leitura do sensor
bool leituraSensor;
bool leituraAnterior;

void setup() {
  
  // Configurações dos pinos
  pinMode(8, INPUT);     // Sensor de umidade do solo
  pinMode(12, OUTPUT);   // Módulo de relé para controlar a bomba
  
  // LEDs indicadores
  pinMode(5, OUTPUT);  // LED vermelho (solo seco)
  pinMode(6, OUTPUT);  // LED azul (bomba ligada)
  pinMode(7, OUTPUT);  // LED verde (solo úmido)
}

void loop() {

  // Leitura do sensor de umidade
  leituraSensor = digitalRead(8);

  if (leituraSensor == HIGH) {
     // Se o solo está seco
     digitalWrite(5, HIGH);  // Liga o LED vermelho
     digitalWrite(7, LOW);   // Desliga o LED verde
  } else {
     // Se o solo está úmido
     digitalWrite(5, LOW);   // Desliga o LED vermelho
     digitalWrite(7, HIGH);  // Liga o LED verde
  }

  // Quando o solo está seco e a leitura anterior era de solo úmido
  if (leituraSensor && !leituraAnterior) {
     delay(5000); // Espera 5 segundos antes de ligar a bomba
     digitalWrite(5, LOW);   // Desliga o LED vermelho
     digitalWrite(6, HIGH);  // Liga o LED azul (indicando bomba ligada)

     while (digitalRead(8)) {
        digitalWrite(12, HIGH);   // Liga a bomba via relé
        delay(500);               // Bomba ligada por 500ms
        digitalWrite(12, LOW);    // Desliga a bomba
        delay(10000);             // Espera 10 segundos antes de nova leitura
     }
     digitalWrite(6, LOW);  // Desliga o LED azul após regar
  }
  
  // Atualiza o estado anterior do sensor
  leituraAnterior = leituraSensor;
}
```

📈 Resultados
O sistema foi testado com sucesso em diferentes níveis de umidade do solo. A bomba d'água foi acionada corretamente quando o solo estava seco, e o feedback visual fornecido pelos LEDs foi eficaz para monitorar o status do solo e da bomba.

🛠️ Desafios e Soluções
Calibração do Sensor: Ajustar o sensor de umidade para diferentes tipos de solo.

Solução: Realizar testes contínuos e ajustes baseados em diferentes condições de solo.
Integração do Relé com a Bomba: Garantir que o relé controle a bomba sem falhas.

Solução: Utilizar um relé de alta qualidade e testar o circuito com diferentes cargas.
🔮 Futuras Melhorias
Controle Remoto: Adicionar controle via Bluetooth ou Wi-Fi para ajustar o sistema remotamente.
Mais Sensores: Integrar sensores adicionais, como temperatura e luz solar, para um controle mais preciso.
