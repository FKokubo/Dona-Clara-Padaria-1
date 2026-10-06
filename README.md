# Dona Clara Panificadora

Web app de encomendas para a Dona Clara, panificadora artesanal de bairro com 12 anos de história.

**Demo:** `https://FKokubo.github.io/dona-clara-panificadora/` (publique com o GitHub Pages, passo a passo abaixo)

## 1. Briefing do problema

A Dona Clara sempre vendeu no balcão e anotava encomendas no caderno da cozinha. Hoje os moradores trabalham em home office, têm horários alternativos e querem garantir o pão ou a encomenda sem fila e sem risco de produto esgotado. O resultado:

- Perda de vendas para duas redes gourmet com forte presença digital, num raio de 2 km.
- Erros em encomendas de eventos (atrasos e troca de sabores) por causa do caderno.
- Nenhum canal para alcançar novos moradores e empresas que buscam coffee break.

Equipe: Clara (produção), Roberto (financeiro), 2 padeiros, 1 confeiteira e 3 atendentes.

## 2. Solução escolhida e justificativa

**Web app (site responsivo com carrinho e painel interno), sem instalação.**

| Alternativa | Por que não |
|---|---|
| Aplicativo móvel | Exige loja de apps, instalação e manutenção. O cliente do bairro não vai baixar um app para comprar pão. |
| Site institucional | Resolve a presença digital, mas não resolve as encomendas nem o caderno. |
| Dashboard interno | Organiza a cozinha, mas não atende o cliente onde ele está. |

O web app atende os dois lados: o cliente monta o pedido pelo celular, e a cozinha acompanha tudo num painel. O pedido é enviado por **WhatsApp**, canal que o casal e os clientes já usam, então não há custo de servidor nem mudança de rotina. Regras de negócio tratam direto a dor das encomendas: antecedência mínima de 48 horas para eventos, quantidade mínima no coffee break e campo de observações para sabores.

## 3. Telas

1. **Cardápio:** produtos por categoria (Pães, Coloniais, Eventos).
2. **Sacola:** itens, total e formulário com nome, WhatsApp, data/hora de retirada e observações.
3. **Painel da cozinha:** pedidos com status (Novo, Em produção, Pronto, Entregue).

> Adicione capturas de tela em `docs/` e referencie aqui: `![Cardápio](docs/cardapio.png)`.

## 4. Arquitetura

- HTML, CSS e JavaScript puros em um único arquivo (`index.html`), sem build e sem dependências.
- **Estado:** `localStorage` do navegador (sacola e pedidos).
- **Envio do pedido:** link `wa.me` com a mensagem formatada.
- **Hospedagem:** GitHub Pages (estático e gratuito).
- Dados do usuário são inseridos com `textContent`, evitando XSS.
- Acessibilidade: foco visível, rótulos ARIA, tema claro/escuro e respeito a `prefers-reduced-motion`.

**Limitação conhecida:** o painel guarda os pedidos no aparelho que os criou. Para o painel receber pedidos de vários clientes, a próxima etapa é um backend (por exemplo Supabase ou Firebase), configurado com variáveis de ambiente e nunca com chaves no código.

## 5. Como executar

Localmente, basta abrir `index.html` no navegador, ou:

```bash
python3 -m http.server 8000   # acesse http://localhost:8000
```

Configuração: em `index.html`, troque a constante `WHATSAPP` pelo número real da padaria (somente dígitos, com DDI e DDD).

### Publicar no GitHub Pages

```bash
git init
git add .
git commit -m "feat: web app de encomendas da Dona Clara"
git branch -M main
git remote add origin https://github.com/Fkokubo/dona-clara-panificadora.git
git push -u origin main
```

Depois, no GitHub: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save**. Em alguns minutos o site fica no ar.

## 6. Segurança

Nenhuma credencial, token ou chave de API está no código ou no histórico. O número de WhatsApp é público por natureza. O `.gitignore` bloqueia `.env`, chaves e `node_modules`.

## 7. Licença

[MIT](LICENSE)
