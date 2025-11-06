# GitRats: Wiki de Desenvolvimento

## 🎯 Visão Geral do Projeto

**GitRats** é uma plataforma gamificada construída para incentivar o desenvolvimento contínuo e de alta qualidade entre programadores. Inspirado na mentalidade "Gym Rat" (dedicação e disciplina), o objetivo é transformar a rotina de programação em uma **Ofensiva (Streak)** constante.

O projeto visa analisar e validar *commits* no GitHub, garantindo que eles atendam a critérios mínimos de qualidade e disciplina (como número de linhas, formatação e padronização) para que sejam contabilizados na sua pontuação diária/semanal.

## ⚙️ Arquitetura e Componentes Principais

A arquitetura do GitRats será dividida em três componentes principais, focados em escalabilidade e desacoplamento:

### 1. Sistema de Observação (Webhook Listener)

* **Função:** Receber e processar eventos (`push` events) enviados pelo GitHub.
* **Tecnologias:** `Node.js`.
* **Processo:**
    1.  O GitHub envia um *payload* para o nosso endpoint.
    2.  O *listener* verifica a autenticidade (assinatura do Webhook).
    3.  Envia os dados brutos do *commit* para a Fila de Processamento.

### 2. Validador de Regras (Core Logic)

* **Função:** O coração do projeto. Aplica as regras de validação definidas.
* **Tecnologias:** `Node.js`.
* **Regras Mínimas de Validação (MVP):**
    * **Tamanho Mínimo:** O *commit* deve adicionar/modificar um mínimo de **X linhas** de código.
    * **Padrão de Mensagem:** A mensagem do *commit* deve seguir um padrão definido (ex: *Conventional Commits* - `feat:`, `fix:`, `chore:`).
    * **Frequência:** Limite de *commits* válidos por dia para evitar *spam*.

### 3. Persistência e Scoreboard

* **Função:** Armazenar dados dos usuários, *commits* validados e gerenciar o *ranking*.
* **Tecnologias:**
    * **Banco de Dados:** `PostgreSQL` (para relações complexas) ou `MongoDB` (para flexibilidade no início).
    * **Frontend:** `React`, `Next.js` e `TailwindCSS` para visualização do *scoreboard*, *landing page* e perfis de usuário.

## 🛣️ Roadmap Inicial (MVP - Produto Mínimo Viável)

| Fase | Objetivo | Entregáveis |
| :--- | :--- | :--- |
| **Fase 1: Configuração** | Configurar ambiente. | Webhook Listener configurado (sem validação), Estrutura básica do banco de dados. |
| **Fase 2: Validação (Core)** | Implementar as regras mínimas de validação. | Validador funcional. Implementação da regra de **Quantidade Mínima de Linhas**. |
| **Fase 3: Scoreboard** | Exibir os resultados e a "Ofensiva" (Streak). | Página inicial do **Scoreboard** (ranking simples). Lógica de cálculo de **Streak** (dias consecutivos com commits validados). |
| **Fase 4: Autenticação** | Permitir que usuários se inscrevam e conectem suas contas GitHub. | Autenticação via **OAuth (GitHub)**. Mapeamento de usuário GitRats para ID do GitHub. |

## 🤝 Contribuições

Este projeto está em estágios iniciais. Contribuições são bem-vindas em qualquer área:

1.  **Ideias de Regras:** Sugestões para novas regras de validação.
2.  **Desenvolvimento:** Implementação dos componentes da arquitetura.
3.  **Design:** Criação da identidade visual e do *layout* do Scoreboard.
