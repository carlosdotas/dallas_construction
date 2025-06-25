# Dallas Construction – Orçamentador de Galpões  
**Projeto Full-Stack • Backend Node.js/Express + Frontend React Native (Android & iOS)**  
> Planejado no modelo **Triângulo de Ferro** (Escopo • Prazo • Recursos)  
> **Prazo-alvo ﹕ 15 dias úteis** a partir do Kick-off (Dia 0)  
> Compilação para **APK** (Android) e **IPA** (iOS) para uso interno – **sem publicação** em lojas.

---

## 1 ▪ Objetivo

1. Aplicativo móvel (RN) para **criar, visualizar e duplicar orçamentos** de galpões metálicos.  
2. Backend **REST** (Node.js + Express + MySQL) responsável por autenticação, cálculo, persistência e geração de **PDF**.  
3. App consome a API, mostra histórico, gera/baixa PDF e armazena sessão JWT de forma segura.  
4. Build de **release** para Android & iOS entregue em artefatos (APK / IPA Ad-hoc ou TestFlight).
5. Link : https://dallas-construction-or-amentador-de-galp-es-960155395693.us-west1.run.app

---

## 2 ▪ Triângulo de Ferro

| Dimensão | Compromisso | Observações |
|----------|-------------|-------------|
| **Escopo / Qualidade** | • Fluxo completo de orçamento (CRUD, cálculo, PDF).<br>• Login (JWT).<br>• Lista com filtros, duplicar, excluir.<br>• Build interno Android e iOS.<br>• UI responsiva (phones/tablets), acessibilidade básica.<br>• Cobertura de testes > 80 % nas regras de cálculo. | Alterar escopo afeta tempo ou recursos. |
| **Prazo / Tempo** | **15 dias úteis** | Mudanças grandes de escopo prolongam prazo; mais devs podem comprimir. |
| **Recursos / Custos** | • 1 Dev Full-Stack Sênior (100 %)<br>• 1 Dev Mobile React Native (80 %)<br>• 1 Designer UI/UX (40 %)<br>• 1 QA (25 %) | Corte de pessoal → risco de qualidade/prazo. |

---

## 3 ▪ Arquitetura

monorepo/
├─ mobile/ # React Native + TypeScript + Expo Router
│ ├─ app/ # / (Dashboard) /orcamento/[id] /novo
│ ├─ components/ # FormSection, BudgetCard, PdfViewer...
│ ├─ hooks/ # useAuth, useBudgets, useForm...
│ └─ ios / android # gerados pelo Expo prebuild
├─ api/ # Node.js 20 + Express + TypeScript
│ ├─ src/
│ │ ├─ controllers/
│ │ ├─ services/ # calculos.ts, pdf.ts
│ │ ├─ routes/
│ │ └─ prisma/
├─ docker-compose.yml
└─ README.md

yaml
Copiar
Editar

### Principais Tecnologias

| Camada | Stack |
|--------|-------|
| **Mobile** | **React Native (Expo SDK ^50)**, Expo Router, React Query, TypeScript, Tailwind (NativeWind), EAS Build |
| **PDF** | Puppeteer (HTML → PDF) |  
| **Backend** | Node.js 20, Express, TypeScript, Prisma ORM, Zod, JWT, Multer (PDF download) |
| **DB** | MySQL 8 (Docker) |
| **CI/CD** | GitHub Actions → lint/test/build + EAS Build triggers |
| **Tests** | Jest + Supertest (API) • Vitest + RTL (mobile logic) |

---

## 4 ▪ Cronograma ﹙15 dias úteis﹚

| Dia | Entrega Parcial | Descrição |
|-----|-----------------|-----------|
| **0** | Kick-off | Repo, Docker skeleton, backlog, Figma link |
| 1-2 | Design System mobile | Paleta, componentes, wireframes RN |
| 3-4 | Backend base | Auth, Prisma schema, CRUD clientes |
| 5-6 | Funções de cálculo + endpoint `/orcamentos` | Testes unitários validados |
| 7-8 | Geração de PDF no backend | Endpoint `/orcamentos/:id/pdf` |
| 9-10 | Telas RN: Login, Dashboard, Form | Form multistep c/ validação Zod |
| 11 | Integração RN ↔ API + resumo em tempo real | React Query cache |
| 12 | Builds de release APK/IPA (EAS) | Docs de instalação |
| 13 | QA, testes e2e (Detox) | Ajustes Lighthouse/PWA não se aplicam |
| 14 | Documentação + CI | README, scripts, GH Actions, seed DB |
| **15** | Handoff final | Tag v1.0.0, entrega APK/IPA, demo via Expo Go |

_Buffer 10 % (≈ 1,5 dia) incluído._

---

## 5 ▪ Backlog Inicial (Issues)

1. **monorepo setup (pnpm + Turbo)**  
2. **docker-compose (api, db, adminer)**  
3. **Auth flow (signup/login, JWT refresh)**  
4. **Budget calculations service & tests**  
5. **PDF renderer & storage**  
6. **React Native navigation & theming**  
7. **Form screens & field masks**  
8. **Offline caching & optimistic updates**  
9. **Dashboard list, filters, swipe actions**  
10. **Duplicate & delete budget endpoints+UI**  
11. **Expo build configs android/ios**  
12. **Detox e2e for “happy path”**  
13. **QA/Accessibility review**  
14. **CI pipeline build & test**  

---

## 6 ▪ Critérios de Aceite

1. **Login** exige credenciais válidas; token salvo com SecureStore.  
2. Criar orçamento → cálculo correto → PDF gerado em < 5 s.  
3. Dashboard exibe lista paginada, permite abrir PDF in-app (WebView).  
4. Build de release assinado (APK + IPA TestFlight/Ad-hoc).  
5. Cobertura > 80 % nas funções críticas.  
6. README: `pnpm i && pnpm dev` (mobile usando Expo Go) + `docker compose up`.  

---

## 7 ▪ Riscos & Mitigações

| Risco | P | I | Mitigação |
|-------|---|---|-----------|
| Problemas de build iOS sem conta Apple | M | M | Usar EAS Simulator build + TestFlight externo; backup via Expo Dev Client |
| Tamanho do PDF > 10 MB mobile | B | M | Otimizar imagens, compressão, stream download |
| Conectividade instável | M | M | Cache local RN + fallback mensagem “tente novamente” |

---

## 8 ▪ Instruções Rápidas

