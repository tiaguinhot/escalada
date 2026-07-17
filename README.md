# 🧗 Retorno à Escalada

App de treino (PWA) para acompanhar um plano de retorno à escalada esportiva após anos parado: 4 semanas de preparação + retorno gradual às vias, com progressão conservadora de dedos.

**Sem framework, sem build, sem servidor** — um único `index.html` com HTML/CSS/JS puro, hospedado como página estática. Os registros sincronizam entre aparelhos via [Supabase](https://supabase.com) (REST/PostgREST).

## Funcionalidades

- **Dois modos numa página só**: celular (app completo) e relógio (Galaxy Watch — timers e registro rápido em botões grandes). Detecção automática pela tela.
- **Plano de 5 treinos/semana**: A (academia) · D (aeróbico + core) · B (fingerboard + tração) · E (antagonistas + panturrilhas) · C (tração pesada), com descansos intercalados e sugestão automática do treino do dia.
- **Timers em tudo que é por tempo**: dead hangs e repeaters 7/3 (séries completas com preparo e descanso), prancha, hollow body, suspensão, aeróbico, mobilidade — tela cheia, com bipes e vibração.
- **Protocolo de fingerboard progressivo** (4 semanas + manutenção), com agarras adaptadas à placa GoUp.
- **Adaptação da sapatilha**: protocolo progressivo de tempo com timer próprio.
- **Registro de treinos e sessões de escalada**: RPE, dor nos dedos, cargas, vias, graus.
- **Offline first**: service worker guarda o app em cache; registros sem conexão ficam pendentes (⏳) e sobem sozinhos quando há internet (☁).
- **Rascunho automático**: treino em andamento não se perde ao fechar a página.

## Arquivos

| Arquivo | Função |
|---|---|
| `index.html` | O app inteiro (celular + relógio) |
| `sw.js` | Service worker — cache offline |
| `manifest.json` | Manifesto PWA (instalação com ícone) |
| `icon-192.png` / `icon-512.png` | Ícones |
| `supabase_schema.sql` | Cria a tabela `treinos` + políticas RLS no Supabase |
| `GUIA_CONFIGURACAO.md` | Passo a passo completo de configuração |

## Configuração

Resumo (detalhes no `GUIA_CONFIGURACAO.md`):

1. **Supabase**: crie um projeto, rode o `supabase_schema.sql` no SQL Editor e copie a *Project URL* e a *Publishable key* (`sb_publishable_...`) para as constantes `SB_URL` e `SB_KEY` no topo do `<script>` do `index.html`. Sem isso o app funciona em modo local (só no aparelho).
2. **Hospedagem**: qualquer serviço de páginas estáticas. Com Cloudflare Pages conectado a este repositório, cada commit republica o app automaticamente.
3. **Instalação**: abra a URL no celular → menu → *Adicionar à tela inicial*. No relógio, abra no navegador — o modo relógio entra sozinho.

Ao atualizar o app, aumente a versão do cache no `sw.js` (`escalada-vN`) para os aparelhos descartarem a versão antiga.

## Segurança

A *Publishable key* do Supabase é feita para ficar visível no navegador; o controle de acesso é das políticas RLS do schema, restritas à tabela `treinos`. O app não guarda dados sensíveis — apenas registros de treino (datas, RPE, vias, observações).

## Licença

Uso pessoal. Fique à vontade para adaptar ao seu próprio retorno às vias. 🧗
