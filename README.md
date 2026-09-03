# 📺 Lumi TV

**Sua TV. Seu jeito.**

Lumi TV é um projeto de plataforma para organização, validação e gerenciamento inteligente de canais de TV ao vivo, desenvolvido para oferecer uma experiência simples, organizada e resiliente em diferentes dispositivos.

Além da infraestrutura de playlists, EPG, monitoramento e failover, estão em desenvolvimento **aplicativos próprios da Lumi TV para Android e Windows/UWP**, criando uma experiência independente e integrada ao ecossistema Lumi TV.

> 🚧 **Projeto em desenvolvimento ativo**

---

## 🚀 Visão do projeto

A Lumi TV está sendo desenvolvida como uma plataforma completa, e não apenas como uma playlist M3U.

A arquitetura do projeto contempla:

- 📺 Canais de TV ao vivo
- 📱 Aplicativo próprio para Android
- 🖥️ Aplicativo para Windows
- 🎮 Aplicativo UWP para dispositivos compatíveis
- 📡 Integração com Kodi / PVR
- 📅 EPG / Guia de Programação
- 🖼️ Logos e metadados
- 🔎 Validação automática de streams
- ❤️ Monitoramento de disponibilidade
- 🔄 Failover inteligente de fontes
- 🌎 Organização por região e praça
- 🌐 Infraestrutura web própria

---

# 📱 Aplicativos Lumi TV

Uma das próximas etapas do projeto é oferecer clientes próprios da Lumi TV.

## Android

Está em desenvolvimento um aplicativo dedicado para dispositivos Android.

A proposta inclui suporte futuro para:

- smartphones;
- tablets;
- Android TV;
- Google TV;
- TV Box.

O aplicativo será integrado à infraestrutura Lumi TV, permitindo que a lógica de canais, grupos, logos, EPG e disponibilidade seja administrada centralmente.

---

## 🖥️ Windows / UWP

Também está em desenvolvimento um cliente Lumi TV para Windows, incluindo estudo e desenvolvimento de uma versão baseada em **UWP (Universal Windows Platform)** para dispositivos compatíveis.

A proposta é permitir uma experiência de TV desenvolvida especificamente para o ecossistema Lumi TV, sem depender exclusivamente de players de terceiros.

A arquitetura está sendo preparada para compartilhar a mesma estrutura de:

```text
Canais
EPG
Logos
Grupos
Status
Primary
Backups
```

entre os diferentes clientes.

---

## 🎮 Xbox / Kodi

Durante a fase atual de desenvolvimento, o Kodi/PVR também é utilizado como plataforma de validação da experiência em TV.

A infraestrutura está sendo preparada para que o usuário visualize apenas o canal:

```text
SBT
RecordTV
Band
TV Cultura
```

e não detalhes técnicos como:

```text
Servidor 1
Servidor 2
Backup
Fonte alternativa
```

A seleção da fonte deve permanecer transparente para o usuário.

---

# 🔄 Failover inteligente

A Lumi TV foi projetada para permitir múltiplas fontes internas para um mesmo canal.

Para o usuário existe apenas:

```text
Canal
```

Internamente:

```text
PRIMARY
   │
   ├── disponível → reproduzir
   │
   └── indisponível
          ↓
      BACKUP 01
          ↓
      BACKUP 02
          ↓
      BACKUP 03
```

O objetivo é permitir que uma fonte alternativa válida possa assumir quando a principal estiver indisponível.

As fontes alternativas permanecem internas e não precisam aparecer como canais duplicados para o usuário.

---

# 📂 Organização dos canais

A estrutura atual prevê grupos como:

```text
Lumi TV | Abertos
Lumi TV | Notícias
Lumi TV | Cultura
Lumi TV | Regionais
Lumi TV | Outros
```

Cada canal lógico pode possuir:

```text
CHANNEL_ID
DISPLAY_NAME
LOGO
GROUP
TVG_ID
EPG
LOCATION
QUALITY
PRIMARY
BACKUPS
STATUS
```

---

# 📊 Validação de streams

A infraestrutura Lumi TV pode analisar as fontes para identificar:

- disponibilidade;
- HTTP/HTTPS;
- HLS;
- resolução real;
- SD / HD / Full HD;
- codec de vídeo;
- codec de áudio;
- FPS;
- bitrate;
- estabilidade;
- redirects;
- CDN;
- provedor do stream;
- estado e cidade;
- compatibilidade provável com PVR.

Sempre que tecnicamente possível, a classificação de qualidade utiliza a **resolução efetivamente entregue pelo stream**, e não apenas informações presentes no nome do canal.

---

# 🌐 Provedores e infraestrutura

A Lumi TV também identifica separadamente:

```text
CHANNEL_OWNER
STREAM_PROVIDER
STREAM_PLATFORM
CDN_HOST
STREAM_TYPE
```

Isso permite diferenciar a emissora responsável pelo conteúdo da infraestrutura utilizada para entregar o vídeo.

Exemplos de tecnologias/plataformas que podem ser identificadas:

```text
HLS
DASH
YouTube
UOL
JMVStream
StreamLock
Akamai
CloudFront
```

---

# 📅 EPG

A Lumi TV possui estrutura para integração com fontes **XMLTV**.

Cada canal pode ser associado a:

```text
tvg-id
tvg-name
tvg-logo
EPG source
```

O sistema procura manter a correspondência correta entre canal, emissora e praça.

Por exemplo, programações de afiliadas ou regiões diferentes não devem ser tratadas automaticamente como equivalentes.

---

# 🖼️ Logos

Os canais preservam sua identidade visual própria.

A marca **Lumi TV** identifica a plataforma, sua tecnologia, organização e experiência.

Ela não substitui nem representa propriedade sobre as marcas das emissoras disponíveis através das fontes utilizadas.

---

# 🏗️ Arquitetura planejada

```text
                     LUMI TV
                        │
              ┌─────────┴─────────┐
              │                   │
          Plataforma          Aplicativos
              │                   │
        ┌─────┼─────┐       ┌─────┼─────┐
        │     │     │       │     │     │
      M3U    EPG  Status  Android Windows UWP
        │
        └── Canais
             │
             ├── Logo
             ├── EPG
             ├── Primary
             ├── Backup 01
             ├── Backup 02
             └── Status
```

---

# 🌐 Infraestrutura Web

Endpoint planejado para a plataforma:

```text
tv.uselumisoft.tech
```

Estrutura prevista:

```text
tv.uselumisoft.tech/
│
├── playlist.m3u
├── epg.xml
├── status.json
├── logos/
└── infraestrutura Lumi TV
```

A infraestrutura web poderá ser utilizada pelos diferentes clientes Lumi TV sem exigir que cada dispositivo mantenha individualmente toda a configuração das fontes.

---

# 🗺️ Roadmap

### Fase atual

- [x] Estrutura inicial Lumi TV
- [x] Parser de playlists
- [x] Validação de streams
- [x] Detecção SD / HD / Full HD
- [x] Identificação de provedores/CDNs
- [x] Estrutura de grupos
- [x] Estrutura Primary / Backup
- [x] Mapeamento inicial de logos
- [ ] Consolidação do EPG
- [ ] Monitoramento contínuo
- [ ] Failover automático
- [ ] Infraestrutura pública Lumi TV

### Aplicativos

- [ ] Lumi TV para Android
- [ ] Lumi TV para Android TV / Google TV
- [ ] Lumi TV para Windows
- [ ] Lumi TV UWP
- [ ] Interface própria de TV
- [ ] Integração centralizada com EPG
- [ ] Favoritos e preferências
- [ ] Sincronização entre dispositivos

---

# ⚠️ Aviso

A Lumi TV é um projeto de software para organização e gerenciamento de fontes de mídia.

Marcas, nomes, logos e conteúdos de terceiros pertencem aos seus respectivos proprietários.

A presença de referências ou metadados neste projeto não implica propriedade, parceria, afiliação ou endosso pelas respectivas emissoras ou plataformas.

O projeto não tem como objetivo contornar DRM, autenticação, restrições de acesso ou outros mecanismos de proteção de conteúdo.

---

# 📺 Lumi TV

### **Sua TV. Seu jeito.**

**Curadoria • Tecnologia • Organização**

Android • Windows • UWP • Kodi/PVR

🚧 **Em desenvolvimento**
