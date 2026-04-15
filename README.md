# 🧮 Calculadora

![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Kotlin](https://img.shields.io/badge/kotlin-%237F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white)

Uma calculadora Android nativa inspirada no design da calculadora do iOS. O aplicativo oferece dois modos de operação — padrão e científico —, um avaliador de expressões com parser recursivo descendente, feedback tátil em todos os botões, histórico persistente e layouts adaptativos para retrato e paisagem.

## 📸 Demonstração
https://github.com/user-attachments/assets/bc977116-947c-49b0-b8cd-3c465f736500
---

## ✨ Funcionalidades

### 🎨 Design e Interface (UI/UX)
* **Tema Imersivo:** Fundo totalmente preto com `statusBarColor` e `navigationBarColor` em `#000000`, criando a ilusão de tela cheia sem usar `WindowInsetsController`.
* **Design System Inspirado no iOS:** Paleta de três cores de botão — cinza escuro para dígitos (`#333333`), cinza claro para ações (AC, +/−, %) e laranja para operadores e `=` (`#FF9500`).
* **Componentes Customizados:** Cada categoria de botão possui um `ShapeDrawable` circular próprio com `<ripple>` para feedback visual de toque dentro dos limites do círculo.
* **Expoentes Visuais:** A expressão `2^3` é exibida no display como `2³`, com suporte a expoentes negativos e compostos (`2⁻¹`, `2⁽³⁺¹⁾`) via mapa de caracteres Unicode superscript.

### ⚙️ Lógica e Regras de Negócio
* **Modo Padrão:** Operações binárias encadeadas (`a OP b =`) com estado mantido em `currentInput`, `operand` e `pendingOp`.
* **Modo Científico:** Ativa 12 botões extras (sin, cos, tan, log, ln, √, π, ℯ, xʸ, `(`, `)`, n!) e delega a avaliação ao `ExprParser`.
* **Parser Recursivo Descendente (`ExprParser`):** Avalia expressões arbitrárias respeitando precedência e associatividade — incluindo associatividade direita para `^` (`2^3^2 = 512`).
* **Feedback Tátil (Haptic):** Todos os botões usam `performHapticFeedback(VIRTUAL_KEY)` via helper de extensão, sem necessidade de permissão `VIBRATE`.
* **Histórico com Bottom Sheet:** Armazena até 50 operações recentes em listas paralelas. Toque em uma entrada restaura o resultado ao display.
* **Preservação de Estado na Rotação:** Todo o estado (input, operando, histórico, modo científico) é persistido via `onSaveInstanceState` e restaurado em `onRestoreInstanceState`.

---

## 📂 Estrutura do Projeto

```text
Calculadora/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/leonardonadson/calculadora/
│   │   │   │   └── MainActivity.kt              # Toda a lógica: motor de cálculo, ExprParser, histórico
│   │   │   ├── res/
│   │   │   │   ├── drawable/
│   │   │   │   │   ├── bg_button_number.xml     # Fundo cinza escuro, circular
│   │   │   │   │   ├── bg_button_operator.xml   # Fundo laranja, circular
│   │   │   │   │   ├── bg_button_action.xml     # Fundo cinza claro, circular
│   │   │   │   │   ├── bg_button_scientific.xml # Fundo cinza grafite, circular
│   │   │   │   │   ├── bg_bottom_sheet.xml      # Painel do histórico arredondado
│   │   │   │   │   ├── ic_history.xml           # Ícone relógio (histórico)
│   │   │   │   │   └── ic_scientific.xml        # Ícone Σ (modo científico)
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml        # Layout portrait
│   │   │   │   │   └── bottom_sheet_history.xml # Bottom Sheet do histórico
│   │   │   │   ├── layout-land/
│   │   │   │   │   └── activity_main.xml        # Layout landscape (painel científico sempre visível)
│   │   │   │   └── values/
│   │   │   │       ├── colors.xml               # Paleta de cores
│   │   │   │       ├── themes.xml               # Estilos e tema da Activity
│   │   │   │       ├── strings.xml              # Textos dos botões
│   │   │   │       └── dimens.xml               # Tamanhos reutilizáveis
│   │   │   └── AndroidManifest.xml              # Configurações globais do Android
│   └── build.gradle.kts                         # Dependências e configurações de build do módulo
└── build.gradle.kts                             # Configurações de build globais do projeto
```

---

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Kotlin
* **SDK:** API 34 (Min: 24)
* **Views e Layouts:** XML (ConstraintLayout, LinearLayout) com qualificadores de recursos (`layout-land/`)
* **Componentes Nativos:** `BottomSheetDialog`, `ConstraintSet` dinâmico, `onSaveInstanceState`
* **Estilização:** Arquivos de `Drawable` customizados com `<ripple>`, `<shape>` oval e `<solid>`
* **Matemática:** `kotlin.math` (sin, cos, tan, log10, ln, sqrt, pow) + `BigDecimal` para formatação
* **IDE:** Android Studio

---

## 💻 Pré-requisitos

Antes de começar, você vai precisar ter instalado em sua máquina:
* [Git](https://git-scm.com) para clonar o repositório.
* [Android Studio](https://developer.android.com/studio) para rodar e editar o código.

## 🚀 Como executar o projeto

1. Abra o seu terminal e faça o clone deste repositório:
   ```bash
   git clone https://github.com/AppLab-Mobile-UFRN-2026-1/App-Calculadora.git
   ```
2. Abra o Android Studio.

3. Na tela inicial, clique em **Open** e selecione a pasta do projeto que você acabou de clonar.

4. Aguarde o Gradle sincronizar todas as dependências.

5. Conecte o seu celular Android via cabo USB ou inicie um Emulador pelo **Device Manager**.

6. Clique no botão verde de **Run** (▶️) na barra superior ou pressione **Shift + F10** para rodar o aplicativo!

---

## 👥 Equipe de Desenvolvimento

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/leonardonadson">
        <img src="https://avatars.githubusercontent.com/leonardonadson" width="100px;" alt="Foto de Leonardo Nadson no GitHub"/>
        <br>
        <sub>
          <b>Leonardo Nadson</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/luan-sampaio">
        <img src="https://avatars.githubusercontent.com/luan-sampaio" width="100px;" alt="Foto de Luan Sampaio no GitHub"/>
        <br>
        <sub>
          <b>Luan Sampaio</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/MarcusAurelius33">
        <img src="https://avatars.githubusercontent.com/MarcusAurelius33" width="100px;" alt="Foto de Marcus Aurelius no GitHub"/>
        <br>
        <sub>
          <b>Marcus Aurelius</b>
        </sub>
      </a>
    </td>
  </tr>
</table>
