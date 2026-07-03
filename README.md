# 🕊️ Aliança 365

Aplicativo web que fortalece **Casal, Filhos e Família através de Deus**.

O casal é o centro. Quando há filhos, o app adapta as atividades pela idade de cada um.
Tudo roda em **um único arquivo** (`index.html`), sem servidor, funcionando no GitHub Pages.

---

## ✨ Funcionalidades

- **Ciclo diário**: 💍 Casal → 👨‍👩‍👧 Família → 👦 Filhos (por idade) → 🙏 Oração → 📖 Palavra → 🌙 Gratidão
- **Filhos por faixa etária**: pequeno (≤5), criança (≤9), pré (≤12) e adolescente — cada um recebe atividade adequada
- **Diário da Família**: todos participam; tudo salvo com data
- **Linha do Tempo**: momentos marcantes por ano, com fotos
- **IA Familiar (Google Gemini)**: descreva uma situação e receba versículo, oração, como conversar e uma atividade — adaptados à idade
- **Desafios semanais**, **Conquistas**, **Sequência de dias** 🔥
- **📕 Livro da Nossa Família**: ao completar a jornada, gera um álbum em PDF com retrospectiva escrita pela IA
- **☁️ Backup no Google Drive**: fotos e registros na sua conta Google
- **📲 PWA**: instale no celular como app, com ícone e funcionamento offline
- **Layout claro e minimalista**

> Sem chave/login configurados, o app funciona 100% offline: a IA usa uma base bíblica local e os dados ficam só no dispositivo (`localStorage`).

---

## 🚀 Publicar no GitHub Pages

### Pelo site (sem instalar nada)
1. Acesse **github.com** → **New repository** → nome `alianca365` → **Public**
2. **Add file → Upload files** → arraste `index.html` (e este `README.md`) → **Commit**
3. **Settings → Pages** → Branch: `main` → pasta `/(root)` → **Save**
4. Aguarde ~1 min → app no ar em `https://SEU-USUARIO.github.io/alianca365`

### Por linha de comando (git)
```bash
git init
git add index.html README.md
git commit -m "Aliança 365"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/alianca365.git
git push -u origin main
# depois: Settings → Pages → Branch main → Save
```

---

## ✨ Configurar a IA (Google Gemini)

Cada família usa a **própria chave** (fica só no aparelho, nunca no repositório). Sem chave, o app usa a base bíblica local offline.

1. Acesse **https://aistudio.google.com/apikey**
2. **Create API key** → copie (começa com `AIza...`)
3. No app: **Mais → Configurações → ✨ IA Familiar** → cole a chave → **Salvar** → **Testar**
4. Escolha o modelo (padrão `gemini-2.5-flash`, rápido e gratuito no nível free)

### 🔒 Segurança da chave Gemini
A chamada sai do navegador, então a chave fica visível para quem usa aquele aparelho. Por isso **cada família usa a sua**. Para blindar contra abuso:

1. **console.cloud.google.com** → APIs e Serviços → Credenciais → sua chave
2. **Restrições de aplicativo** → "Referenciadores HTTP" → adicione `https://SEU-USUARIO.github.io/*`
3. **Restrições de API** → apenas **Generative Language API**

Assim a chave só funciona a partir do seu site.

---

## ☁️ Configurar Backup no Google Drive

O Drive exige um **OAuth Client ID** (diferente da API key do Gemini). O app usa o escopo `drive.file` — **só acessa arquivos que ele mesmo cria**, nunca o resto do seu Drive.

### Passo a passo (uma vez) — em **console.cloud.google.com**
1. Crie um projeto (ou use um existente)
2. **APIs e Serviços → Biblioteca** → ative **Google Drive API**
3. **Tela de consentimento OAuth**:
   - Tipo de usuário: **Externo**
   - Preencha nome do app + seu email
   - Em **Usuários de teste**, **adicione o seu Gmail** (sem isso, o login é bloqueado)
4. **Credenciais → Criar credenciais → ID do cliente OAuth**:
   - Tipo de aplicativo: **Aplicativo da Web**
   - **Origens JavaScript autorizadas**: `https://SEU-USUARIO.github.io`
   - (não precisa preencher "URIs de redirecionamento")
5. Copie o **ID do cliente** (termina em `.apps.googleusercontent.com`)
6. No app: **Mais → Configurações → ☁️ Backup no Google Drive** → cole o ID → **Conectar Google Drive**

### Como usar
- **⬆️ Enviar backup**: cria a pasta `Aliança 365` no seu Drive, sobe `alianca365-backup.json` (todos os registros) e cada foto da timeline como JPG
- **⬇️ Restaurar**: baixa o backup em outro aparelho (mantém as chaves locais deste aparelho)
- **Backup automático**: liga o toggle para salvar ao registrar diário, gratidão ou momento

### ⚠️ Pontos importantes
- OAuth exige **HTTPS + origem autorizada** → funciona na URL do **GitHub Pages**, **não** abrindo o arquivo local (`file://`). Para testar localmente, rode um servidor (`python -m http.server`) e adicione `http://localhost:8000` às origens autorizadas.
- O token dura ~1 hora; o app renova sozinho durante a sessão.
- Em "modo de teste" no Google, só os **usuários de teste** cadastrados conseguem entrar (suficiente para a família). Publicar o app remove esse limite, mas o Google pede verificação.
- O arquivo de backup **não** contém a chave Gemini nem o Client ID (segredos ficam só no aparelho).

---

## 📲 Instalar no celular (PWA)

O app é um **Progressive Web App**: instala como aplicativo, com ícone na tela inicial e funcionamento offline (o conteúdo diário e a IA local funcionam sem internet).

- **Android (Chrome)**: abra o site → aparece o botão **📲 Instalar Aliança 365** (ou menu ⋮ → "Instalar app" / "Adicionar à tela inicial").
- **iPhone (Safari)**: botão **Compartilhar** → **Adicionar à Tela de Início**.
- **Desktop (Chrome/Edge)**: ícone de instalar na barra de endereço.

> PWA exige **HTTPS** → funciona na URL do GitHub Pages. Abrir o arquivo local (`file://`) não instala.
> O que precisa de internet: IA Gemini (respostas por IA), backup no Drive e o SDK de login do Google. O resto roda offline.

---

## 🔐 Privacidade

- Todos os dados ficam no **`localStorage` do navegador** (só no aparelho).
- A situação enviada à IA vai à **API do Google** apenas quando há chave configurada.
- O backup vai **para o seu próprio Google Drive**, na sua conta.
- Nenhum dado passa por servidores de terceiros além do Google (Gemini/Drive), sob suas próprias credenciais.

---

## 🛠️ Estrutura

```
index.html             → o app inteiro (HTML + CSS + JS)
manifest.webmanifest   → metadados do PWA (nome, ícones, cores)
sw.js                  → service worker (cache offline do app)
icon-192.png           → ícone do app (192x192)
icon-512.png           → ícone do app (512x512)
README.md              → este guia
```

> **Importante**: para o PWA e o backup funcionarem, envie **todos** esses arquivos ao repositório, não só o `index.html`.

Bibliotecas externas: apenas o **Google Identity Services** (`accounts.google.com/gsi/client`), usado no login do Drive. A IA (Gemini) e o Drive são chamados via `fetch` direto do navegador.

---

*"Eu e minha casa serviremos ao Senhor." — Josué 24:15* 🕊️
