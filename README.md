# Action Log

Sistema de registro e acompanhamento de demandas técnicas de manutenção predial. Cadastro, priorização e histórico de atividades, com acesso multiusuário e multi-empreendimento.

Demo: **https://oliverprioli.github.io/action-log/**

---

## O que faz

Cada usuário loga e enxerga apenas os empreendimentos aos quais está vinculado. Dentro de um empreendimento, é possível registrar, filtrar, editar e finalizar ações técnicas, associadas a sistemas prediais (CFTV, controle de acesso, automação predial, telefonia, infraestrutura, entre outros).

Cada ação recebe um código sequencial gerado automaticamente, com prefixo próprio por empreendimento.

---

## Stack

| Camada | Tecnologia |
|---|---|
| Frontend | HTML/CSS/JS único, sem build, sem framework |
| Hospedagem | GitHub Pages |
| Backend | Supabase (Postgres + Auth) |
| Autenticação | E-mail e senha |
| Controle de acesso | Row Level Security (RLS) no banco |

Não há servidor próprio: o navegador fala diretamente com o Supabase usando uma chave pública, segura para ficar exposta — quem decide o que cada usuário vê é o RLS no banco, não o sigilo da chave.

---

## Modelo de dados (resumo)

- **Empreendimentos** — as unidades geridas, cada uma com prefixo de código próprio.
- **Vínculos usuário↔empreendimento** — controla quem vê o quê, com papel (técnico/supervisor).
- **Responsáveis** — pessoas ou equipes responsáveis por uma ação, específicas de um empreendimento ou globais.
- **Ações** — os registros: sistema, descrição, diagnóstico, ação executada, responsável, prioridade, categoria, status, datas e localização.

O isolamento entre empreendimentos é garantido no banco via RLS, não na interface — mesmo que alguém manipule a página, o servidor não devolve dado de um empreendimento ao qual o usuário não está vinculado.

---

## Cadastro de usuários

Feito manualmente por um administrador; não há auto-cadastro público.

---

## Status

Projeto pessoal em uso ativo, em desenvolvimento contínuo.
