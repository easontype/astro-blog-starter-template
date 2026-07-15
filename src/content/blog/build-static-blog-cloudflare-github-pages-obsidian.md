---
title: 免費架一個靜態部落格：Cloudflare 買網域 + GitHub Pages + Obsidian 寫文章，5 步驟不用 30 分鐘
description: 不需要額外付費或登入功能的後台，材料所研究生真人示範用 5 個步驟把部落格架起來，這個網站 aibazhaocat.com 本身就是這樣上線的。
pubDate: 2026-07-15T09:00:00+08:00
tags: ["建站教學", "AI學習"]
---

<!-- TODO: 補上完整流程總覽截圖或跳過，直接進步驟 -->

材料所研究生一枚，前陣子想把部落格從 GitHub 預設的 `xxx.github.io` 換成自己的網域，查了一輪發現不用架伺服器、不用資料庫、不用月費主機，全程免費（除了網域本身），流程走完不用 30 分鐘。這篇就是完整拆解，照著做就好。

[Threads傳送門](https://www.threads.com/@pro_ai.news)

用的工具只有四個：Cloudflare（買網域＋設定 DNS）、GitHub（放程式碼＋免費架站）、Obsidian（純筆記軟體，拿來當寫文章的後台）、還有一個 AI coding 工具（把網站框架生出來）。這個網站本身就是這樣架的。

## 1. 到 Cloudflare 買一個網域

- **費用：** `.com`／`.blog` 這類常見後綴相對便宜，年費大概落在新台幣 300–500 元
- **平台：** Cloudflare Registrar，不用另外找其他註冊商，買完網域跟後面的 DNS 設定會在同一個地方管理
- **注意：** 網域名稱決定了之後所有連結，先想好帳號一致的名字再買

Cloudflare 網域註冊入口：[Cloudflare Registrar](https://www.cloudflare.com/products/registrar/)

<!-- TODO: 插入 Cloudflare 購買網域畫面截圖 -->

如果連這筆網域費都想省，也有兩個真正免費、不用申請的選項：

- **GitHub Pages 內建的網域：** repo 開啟 GitHub Pages 之後，本來就會有一個 `使用者名稱.github.io` 可以直接用，不用申請也不用設定，這篇文章要換掉的其實就是這個網址
- **Cloudflare Pages 附贈的網域：** 如果改用 Cloudflare Pages（不是本文用的 GitHub Pages）架站，部署完會自動給一個 `專案名稱.pages.dev`，一樣不用申請或付費，只是架站流程跟後面第 2–4 步不同

這兩個都是架站服務內建送的網域，缺點是網址比較長、比較沒有品牌感。先用免費的把整套流程跑一次，之後想換自訂網域，回頭做第 1 步跟第 4 步就好。

## 2. 在 GitHub 建立一個 public repo

- **限制：** 一定要是 public repo，GitHub Pages 免費方案不支援 private repo 架站
- **內容：** repo 裡放的就是你的網站程式碼（可以請 AI coding 工具幫你生一個靜態網站框架，例如 Astro、Next.js 靜態匯出）
- **命名：** repo 名稱隨意，不影響最終網域

<!-- TODO: 插入 GitHub 建立 public repo 畫面截圖 -->

## 3. 在 GitHub repo 設定 custom domain

- **路徑：** repo 頁面 → Settings → Pages
- **動作：** 在 Custom domain 欄位填入你買的網域，存檔
- **效果：** GitHub 會產生一個根目錄 `CNAME` 檔案記錄這個網域，這步做完網域還不會生效，要等第 4 步 DNS 設定完成

<!-- TODO: 插入 GitHub Pages Custom domain 設定畫面截圖 -->

## 4. 回 Cloudflare 設定 DNS records

- **路徑：** Cloudflare 你買的網域 → DNS → Records
- **要加的紀錄：** 4 筆 A record 指向 GitHub Pages 的固定 IP（185.199.108.153／185.199.109.153／185.199.110.153／185.199.111.153），如果要讓 `www` 也能訪問，再加一筆 CNAME 指到你的 `xxx.github.io`
- **Proxy status 務必設「DNS only」**（灰色雲朵，不要橘色）——橘色代表 Cloudflare 幫你代理流量，會跟 GitHub Pages 自己的 SSL 憑證衝突
- **等待：** DNS 生效通常幾分鐘到幾小時，生效後回 GitHub Pages 設定勾選 Enforce HTTPS

<!-- TODO: 插入 Cloudflare DNS records 設定畫面截圖 -->

## 5. 讓 AI 把部落格框架建起來，Obsidian 當後台寫文章

- **建框架：** 跟 AI coding 工具說你要一個靜態部落格網站，它可以直接生出首頁、文章列表、文章頁的程式碼
- **寫文章：** 不需要額外的後台系統，Obsidian 本身就是純 markdown 筆記軟體，直接把 vault 資料夾對應到網站程式碼裡放文章的資料夾（例如 `src/content/blog/`），寫完存檔、推上 GitHub，網站就會自動重新部署
- **好處：** 沒有登入頁面、沒有資料庫、沒有額外費用，內容本身就是純文字檔，方便版本控制也方便之後搬家

<!-- TODO: 插入 Obsidian 寫文章畫面截圖 -->

## 整體流程

5 步驟走完，網域從購買到部落格正式上線，實際操作時間不用 30 分鐘（DNS 生效等待時間不算）。整套流程沒有任何一步需要額外付費的後台服務或登入系統，收藏起來，之後想架自己的網站可以直接照做。

有卡住的地方，或想看更完整的技術細節，歡迎來 [Threads](https://www.threads.com/@pro_ai.news) 留言。
