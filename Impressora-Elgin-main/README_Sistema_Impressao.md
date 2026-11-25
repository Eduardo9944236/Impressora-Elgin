# 🖨️ Sistema de Impressão Elgin i8/i9 em C
### *(Aplicação de terminal para comunicação com impressoras térmicas Elgin)*
---

## 📘 Sobre o Projeto

Este projeto consiste em uma aplicação desenvolvida em **C** que permite a comunicação com impressoras térmicas **Elgin i8 e i9**. O sistema utiliza a **DLL do fabricante** para configurar a conexão, realizar diferentes tipos de impressão e controlar periféricos compatíveis.

A interação com o programa acontece pelo terminal, por meio de um menu de opções. Entre os recursos disponíveis estão a impressão de textos, QR Codes, códigos de barras e documentos SAT, além do acionamento de gavetas e do sinal sonoro da impressora.

---

## 🧰 Tecnologias e Requisitos

- **Linguagem C**
- **Executar com dev-c++
- **Windows**, com suporte às APIs de `windows.h`
- **DLL/SDK do fabricante Elgin**, compatível com a arquitetura do compilador
- **Impressora térmica Elgin i8 ou i9**, conectada por USB
- Arquivos `XMLSAT.xml` e/ou `CANC_SAT.xml`, caso sejam utilizadas as funções de impressão SAT

> ⚠️ A impressora precisa estar ligada e conectada para que as operações de comunicação e impressão funcionem. Os nomes das portas e os parâmetros utilizados devem corresponder à configuração do equipamento.

---

## 📁 Arquivos Necessários

- `main.c` → Arquivo principal do código-fonte.
- `E1_Impressora01.dll` → Biblioteca do fabricante, escolhida de acordo com a arquitetura do compilador.
- `impressora.exe` → Executável gerado após a compilação.
- `XMLSAT.xml` → Arquivo utilizado na impressão do cupom fiscal SAT.
- `CANC_SAT.xml` → Arquivo utilizado na impressão do comprovante de cancelamento SAT.

A DLL deve ficar na pasta principal do projeto, junto ao executável. Os arquivos XML precisam estar na pasta de execução quando suas respectivas opções forem utilizadas.

---

## ⚙️ Instalação e Execução


Escolha a DLL que tenha a mesma arquitetura indicada pelo compilador:

- Se o resultado apresentar `x86_64`, utilize `E1_Impressora01.dll` da pasta **x64**.
- Se aparecer `mingw32` ou `i686`, utilize `E1_Impressora01.dll` da pasta **x86**.


Se a compilação terminar sem erros, o arquivo `impressora.exe` será criado no mesmo diretório. Caso o projeto utilize outros arquivos de código ou bibliotecas, eles também deverão ser incluídos no comando conforme a configuração utilizada.

### ▶️Iniciar a aplicação

No Prompt de Comando ou PowerShell, execute:

```powershell
.\impressora.exe
```

No Git Bash, também é possível iniciar o programa com:

```bash
./impressora.exe
```

Mantenha a DLL selecionada na mesma pasta do executável para que ela possa ser localizada durante a inicialização.

---

## 🔐 Acesso ao Sistema

Ao abrir o programa, o operador deverá informar as credenciais de acesso. São permitidas até **três tentativas** antes do encerramento da aplicação.

- **Usuário:** `admin`
- **Senha:** `1234`

Essas são as credenciais padrão desta versão e devem ser consideradas apenas para demonstração. Não são adequadas para proteger dados ou garantir controle de acesso em um ambiente de produção. Se o programa permitir, altere os dados diretamente no código antes de distribuir a aplicação.

---

## 🧪 Funcionalidades do Sistema

Depois de realizar o login, escolha no terminal o número correspondente à operação desejada.

| Tecla | Funcionalidade | Descrição |
| --- | --- | --- |
| `1` | Configurar conexão | Define a porta (por exemplo, `USB`), o modelo da impressora (`i8` ou `i9`) e os parâmetros técnicos necessários. |
| `2` | Abrir conexão | Inicia a comunicação com a impressora usando a configuração selecionada. |
| `3` | Fechar conexão | Finaliza a comunicação e libera a porta USB ou serial. |
| `4` | Imprimir texto | Envia uma mensagem para impressão e solicita o corte do papel. |
| `5` | Imprimir QR Code | Imprime um QR Code no papel térmico e solicita o corte. |
| `6` | Imprimir código de barras | Imprime um código no padrão **CODE 128**, com sua numeração visível, e solicita o corte. |
| `7` | Imprimir XML SAT | Lê `XMLSAT.xml` e imprime o cupom fiscal formatado. |
| `8` | Imprimir cancelamento SAT | Lê `CANC_SAT.xml` e imprime o comprovante de cancelamento com QR Code de assinatura. |
| `9` | Abrir gaveta (Elgin) | Envia o pulso de acionamento destinado às gavetas de dinheiro Elgin. |
| `10` | Abrir gaveta (padrão) | Envia um pulso padrão para gavetas convencionais compatíveis. |
| `11` | Emitir sinal sonoro | Aciona o buzzer interno da impressora conforme a quantidade solicitada. |
| `0` | Sair | Fecha uma conexão ativa, libera a DLL e encerra o programa. |

> 🔌 As operações de impressão e acionamento de periféricos exigem uma conexão ativa. Antes de utilizá-las, configure a conexão e execute a opção `2` do menu.

---

## 🛠️ Validações e Diagnóstico

- **Operações sem conexão:** os comandos de impressão e abertura de gaveta são impedidos quando a conexão não está ativa. O sistema informa que a operação não pode ser realizada nessa condição.
- **Validação de números:** a função `lerInteiro` verifica entradas inválidas, como letras ou símbolos em campos numéricos, e solicita uma nova informação.
- **Retornos da DLL:** as respostas das operações são verificadas. Quando ocorre uma falha, como falta de papel ou desconexão do cabo, o programa apresenta o código numérico retornado pela DLL para ajudar na identificação do problema.

---

## 🧩 Solução de Problemas

- **A impressora não responde:** confirme se está ligada, conectada e configurada na porta correta. Verifique também se a opção **Abrir conexão** foi executada.
- **Erro na impressão do XML SAT:** confira o nome do arquivo e se ele está na pasta em que o programa foi iniciado.

---

## 👥 Autores

- Eduardo de França
- Gustavo Tavares
- Henrique Alves

---
