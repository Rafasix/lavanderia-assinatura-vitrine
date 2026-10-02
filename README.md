# 🧺 Plataforma de lavanderia com coleta e entrega

> **Projeto real em desenvolvimento.** Nome, marca e dados do negócio foram omitidos por confidencialidade.
> Este repositório é uma **vitrine**: mostra o que foi construído e como funciona, sem o código-fonte.

O cliente agenda, o motorista busca, a unidade pesa, lava e devolve, e cada etapa fica registrada.

**Meu papel:** desenvolvimento, com agentes de IA (Claude Code) escrevendo o código sob a minha orientação. Defino a arquitetura, valido o que é gerado e publico.

---

## 📱 Telas do app do cliente

<table>
  <tr>
    <td><img src="telas/01-inicio.jpg" width="170" alt="Tela inicial"></td>
    <td><img src="telas/02-servicos.jpg" width="170" alt="Serviços e pedidos"></td>
    <td><img src="telas/05-agendar.jpg" width="170" alt="Agendar coleta"></td>
    <td><img src="telas/03-pedidos.jpg" width="170" alt="Acompanhar pedido"></td>
    <td><img src="telas/04-plano.jpg" width="170" alt="Meu plano"></td>
  </tr>
  <tr>
    <td align="center">Início</td>
    <td align="center">Serviços</td>
    <td align="center">Agendar coleta</td>
    <td align="center">Pedidos</td>
    <td align="center">Plano</td>
  </tr>
</table>

---

## 🧩 Três aplicações, um banco de dados

As três áreas leem e gravam no mesmo banco, em tempo real. O que o motorista toca na rua aparece na hora no painel da loja e no app do cliente.

| Aplicação | Quem usa | O que faz |
|---|---|---|
| **App do cliente** | Cliente | Agenda a coleta por dia e período e acompanha o pedido, da saída do motorista até o peso na balança |
| **Painel do operador** | Equipe da loja | Fila de trabalho do dia, confirmação dos pedidos, recebimento, pesagem e gestão de clientes, imóveis, rotas e equipe |
| **App do motorista** | Motorista | Duas listas, o que buscar e o que entregar, com um toque em cada parada |

Cada pessoa só enxerga o que precisa: são **8 papéis de acesso**, e uma mesma pessoa pode acumular mais de um.

### Fluxo do pedido

```
solicitar → confirmar → rota → coletar → receber → pesar → triagem
→ lavar → secar → controle de qualidade → dobrar → expedir → entregar → concluir
```

Cada transição grava **quem fez, quando e em qual unidade**.

---

## 🛠️ Stack

| Camada | Tecnologia |
|---|---|
| Web (painel e app) | Next.js 16 · React 19 · TypeScript |
| Banco, autenticação, storage | Supabase (PostgreSQL) |
| App Android | Capacitor |
| Deploy contínuo (CD) | GitHub + Netlify |
| Integração contínua (CI) | GitHub Actions |

---

## 🔒 Qualidade e segurança

Regras do projeto:

- **Isolamento entre unidades** feito dentro do banco (Row Level Security), nunca pelo aplicativo
- **Toda tabela com política de acesso.** O CI falha se aparecer uma tabela sem proteção
- **Nenhuma chave no repositório**
- **Financeiro imutável:** correção é sempre um lançamento novo
- **Auditoria com antes e depois** em pesagem, status, cobrança e ocorrências
- **Nada fixo no código:** preço, franquia e prazos são parâmetros de cada unidade

**Pipeline de CI:** a cada mudança no banco, o GitHub Actions sobe um PostgreSQL, aplica todas as migrations e roda os testes de proteção e de isolamento entre unidades.

---

## 📊 Números do projeto

| | |
|---|---|
| Telas | 33 |
| Aplicações | 3 (cliente, operador, motorista) |
| Migrations do banco | 30 |
| Papéis de acesso | 8 |
| Etapas do fluxo do pedido | 14 |

---

---

Feito por **Rafael Sisti** · [LinkedIn](https://www.linkedin.com/in/rafaelhsn) · [GitHub](https://github.com/Rafasix)
