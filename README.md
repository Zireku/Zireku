<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=220&color=0:0f0c29,50:302b63,100:24243e&text=Zireku&fontColor=ffffff&fontSize=64&fontAlignY=38&desc=Full-Stack%20Developer%20%C2%B7%20Bot%20Architecture%20Specialist&descAlignY=58&descSize=16&animation=fadeIn" alt="Zireku" width="100%" />

<a href="https://github.com/Zireku">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=18&duration=3200&pause=900&color=A78BFA&center=true&vCenter=true&width=620&lines=Canvas+graphic+engines+that+render+pixel-accurate;Real-time+messaging+bots+that+don't+fall+over;Automation+that+keeps+running+while+I+sleep" alt="typing intro" />
</a>

<br/>

[![Website](https://img.shields.io/badge/zireku.com-0f0c29?style=for-the-badge&logo=googlechrome&logoColor=a78bfa)](https://zireku.com)
[![GitHub followers](https://img.shields.io/github/followers/Zireku?style=for-the-badge&logo=github&color=302b63&labelColor=0f0c29)](https://github.com/Zireku)
[![Profile views](https://hits.sh/github.com/Zireku.svg?style=for-the-badge&color=302b63&labelColor=0f0c29&label=VIEWS)](https://hits.sh/github.com/Zireku/)

</div>

---

## About

I build things that draw images and talk to people, usually at the same time.

Most of my work sits between two worlds: a **canvas rendering engine** that has to match a real UI down to the pixel, and a **messaging bot** that has to answer in under a second while hundreds of chats are hitting it. I care about the boring parts that make those two things reliable: queues, retries, memory, deploys.

---

## Featured project

### [`smsvirtual.web-showcase`](https://github.com/Zireku/smsvirtual.web-showcase)

Enterprise virtual number and realtime SMS OTP verification platform with multi-provider failover (NusaOTP & OTPMurah), automated Midtrans payments (QRIS & Virtual Accounts), and zero-refresh Server-Sent Events (SSE). Built with Nuxt 3 SSR, Nitro engine, and MongoDB Atlas with Optimistic Concurrency Control.

* **Live Demo**: [https://otp.zireku.com](https://otp.zireku.com)
* **Architecture**: Nuxt 3 Universal SSR · Nitro Engine · Server-Sent Events · Midtrans Webhook Gateway · Cloudflare Tunnel

```mermaid
flowchart LR
    User([End User]) --> CF[Cloudflare Tunnel]
    CF --> Nuxt[Nuxt 3 SSR & Nitro Engine]
    Nuxt --> SSE[Server-Sent Events Bus]
    Nuxt --> DB[(MongoDB Atlas OCC)]

    Nuxt --> Midtrans{Midtrans Gateway}
    Midtrans -->|QRIS / VA Webhook| Nuxt

    Nuxt --> ProviderPool{Provider Pool}
    ProviderPool -->|Failover| P1[NusaOTP API]
    ProviderPool -->|Failover| P2[OTPMurah API]

    P1 -->|Incoming OTP| Nuxt
    P2 -->|Incoming OTP| Nuxt
    Nuxt -->|Instant Push| SSE
    SSE -->|Live Code| User

    classDef edge fill:#1e1b4b,stroke:#a78bfa,color:#fff;
    classDef core fill:#302b63,stroke:#a78bfa,color:#fff;
    class User,Midtrans edge;
    class CF,Nuxt,SSE,DB,ProviderPool,P1,P2 core;
```

---

### [`zireku-canvas`](https://github.com/Zireku/zireku-canvas)

A pixel-accurate renderer for WhatsApp iOS-style quote bubbles, channel and group info cards, a QRIS builder, and a social media showcase generator. It runs on `@napi-rs/canvas`, with its own typography layer for text wrapping, emoji and mixed-script handling.

```mermaid
flowchart LR
    A([WhatsApp message]) --> B[Baileys socket]
    B --> C{Command router}
    C -->|quote / card / qris| D[(Task queue)]
    D --> E[Canvas worker]

    subgraph Engine [zireku-canvas]
        direction TB
        E --> F[Layout + typography]
        F --> G[Image processing]
        G --> H[SVG + canvas compositing]
    end

    H --> I[PNG / WebP buffer]
    I --> J[Send back to chat]

    K([REST client]) --> L[Nginx + Cloudflare]
    L --> M[Express API]
    M --> D

    classDef edge fill:#1e1b4b,stroke:#a78bfa,color:#fff;
    classDef core fill:#302b63,stroke:#a78bfa,color:#fff;
    class A,K edge;
    class B,C,D,E,M core;
```

The same engine sits behind both the bot and the HTTP API, so a quote rendered in a chat and one fetched from an endpoint come out identical.

---

## Stack

<div align="center">

| | |
|:--|:--|
| **Core & Backend** | ![JavaScript](https://img.shields.io/badge/JavaScript_ES6+-1e1b4b?style=flat-square&logo=javascript&logoColor=F7DF1E) ![TypeScript](https://img.shields.io/badge/TypeScript-1e1b4b?style=flat-square&logo=typescript&logoColor=3178C6) ![Node.js](https://img.shields.io/badge/Node.js-1e1b4b?style=flat-square&logo=nodedotjs&logoColor=5FA04E) ![Nuxt](https://img.shields.io/badge/Nuxt_3-1e1b4b?style=flat-square&logo=nuxtdotjs&logoColor=00DC82) ![Vue.js](https://img.shields.io/badge/Vue.js-1e1b4b?style=flat-square&logo=vuedotjs&logoColor=4FC08D) ![Express](https://img.shields.io/badge/Express-1e1b4b?style=flat-square&logo=express&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-1e1b4b?style=flat-square&logo=mongodb&logoColor=47A248) ![REST](https://img.shields.io/badge/REST_APIs-1e1b4b?style=flat-square&logo=postman&logoColor=FF6C37) |
| **Graphics & Media** | ![Canvas](https://img.shields.io/badge/@napi--rs/canvas-1e1b4b?style=flat-square&logo=html5&logoColor=E34F26) ![SVG](https://img.shields.io/badge/SVG-1e1b4b?style=flat-square&logo=svg&logoColor=FFB13B) ![Image Processing](https://img.shields.io/badge/Image_Processing-1e1b4b?style=flat-square&logo=files&logoColor=a78bfa) ![Typography](https://img.shields.io/badge/Typography_Engine-1e1b4b?style=flat-square&logo=fontforge&logoColor=a78bfa) |
| **Automation & Bots** | ![Baileys](https://img.shields.io/badge/WhatsApp_Baileys-1e1b4b?style=flat-square&logo=whatsapp&logoColor=25D366) ![WebSockets](https://img.shields.io/badge/WebSockets-1e1b4b?style=flat-square&logo=socketdotio&logoColor=white) ![Webhooks](https://img.shields.io/badge/Webhooks-1e1b4b?style=flat-square&logo=webhooks&logoColor=C73A63) ![Queues](https://img.shields.io/badge/Task_Queues-1e1b4b?style=flat-square&logo=rabbitmq&logoColor=FF6600) |
| **DevOps & Infra** | ![Linux](https://img.shields.io/badge/Ubuntu_/_Debian-1e1b4b?style=flat-square&logo=linux&logoColor=FCC624) ![PM2](https://img.shields.io/badge/PM2-1e1b4b?style=flat-square&logo=pm2&logoColor=2B037A) ![Git](https://img.shields.io/badge/Git-1e1b4b?style=flat-square&logo=git&logoColor=F05032) ![Nginx](https://img.shields.io/badge/Nginx-1e1b4b?style=flat-square&logo=nginx&logoColor=009639) ![Cloudflare](https://img.shields.io/badge/Cloudflare-1e1b4b?style=flat-square&logo=cloudflare&logoColor=F38020) |

</div>

---

## GitHub stats

<div align="center">

<a href="https://github.com/Zireku">
  <img height="170" src="https://github-readme-stats.vercel.app/api?username=Zireku&show_icons=true&hide_border=true&bg_color=0f0c29&title_color=a78bfa&icon_color=a78bfa&text_color=d6d3f0&ring_color=a78bfa&count_private=true&include_all_commits=true" alt="GitHub stats" />
</a>
<a href="https://github.com/Zireku">
  <img height="170" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Zireku&layout=compact&hide_border=true&bg_color=0f0c29&title_color=a78bfa&text_color=d6d3f0&langs_count=6" alt="Top languages" />
</a>

<br/>

<img src="https://streak-stats.demolab.com?user=Zireku&hide_border=true&background=0f0c29&ring=a78bfa&fire=a78bfa&currStreakLabel=d6d3f0&sideLabels=d6d3f0&currStreakNum=ffffff&sideNums=ffffff&dates=8b86b3" alt="Contribution streak" />

</div>

---

## Contributions

<div align="center">

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Zireku&bg_color=0f0c29&color=d6d3f0&line=a78bfa&point=ffffff&area=true&area_color=a78bfa&hide_border=true&radius=8" alt="Contribution activity graph" width="100%" />

<br/><br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Zireku/Zireku/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Zireku/Zireku/output/github-snake.svg" />
  <img alt="Contribution snake" src="https://raw.githubusercontent.com/Zireku/Zireku/output/github-snake-dark.svg" width="100%" />
</picture>

</div>

---

## Find me

<div align="center">

[![zireku.com](https://img.shields.io/badge/Website-zireku.com-302b63?style=for-the-badge&logo=googlechrome&logoColor=white)](https://zireku.com)
[![GitHub](https://img.shields.io/badge/GitHub-@Zireku-302b63?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Zireku)

<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&height=110&color=0:24243e,50:302b63,100:0f0c29&section=footer" width="100%" alt="" />

</div>
