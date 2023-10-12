---
title: Next.JS Deployment
date: 2022-12-11 20:58:54
tags:
- web
- vercel
- programming
---
## Next.JS Deployment

Ahoj, tady zas a znova Vítek, dneska se tady chci rozepsat o tom jak jsem deploynul NExt.JS aplikaci (tento web) za použití Githubu a Vercelu. 

## Než začneme

Takže, před tím než začneme, budeme potřebovat zaregistrovat se na pár stránkách, takže pojďme na to.
    1. [Github](https://github.com/) - Pro ty co neví co je Github, tak je to git server, můžete zde mít repositáře, a můžete díky němu používat Git Version Controll. Je to užitečná stránka, tak se zaregistrujte :D.
    2. [Vercel](https://vercel.app) - Tvůrce NExt.JS, tato stránka vám také umožní deploynout svoje NExt.JS aplikace (weby). Takže jej použijeme
    3. Freenom - TOTO NENÍ NUTNÉ, ale, tato stránka vám umožní si vydat vlastní doménu zdarma až na 12 měsíců, od nich mám doménu www.smoliicek.tk.

Když máme toto připraveno tak musíme vytvořit naší NExt.JS app, to uděláme pomocí

``` bash
$ npx create-next-app
```

Zvolíme jestli chceme použít TS a zvolíme název našeho projektu

## Github Repo

Poté co máme vytvořenou naši NExt.js aplikaci a uděláme úpravy které chceme deploynout (UPOZORNĚNÍ - tohle není next.js tutoriál, najděte si něco na YT). Před tím než toto ale uděláme, musíme dostat náš kód na github. Takže pojďme na to!

Takže poté co si vytvoříme repositár na Githubu na [https://github.com/new](https://github.com/new) tak do něj můžeme pushnout náš kód. Spustíme tedy proto příkaz

``` bash
$ git add . && git commit -m (SemSiNapišteCokolivAleNezapomeňteŽeTotoBudeVidětNaGithubu) && git push main
```

## Vercel Deployment

Poté co toto uděláme, přejdeme na [https://vercel.com/](https://vercel.com/) a zaregistrujeme se přez Github. Poté se dostaneme na náš dashboard, klikneme na continue with github a můžeme Vercelu dát přístup k našemu repositáři s naším webem. Autorizujeme Vercel bota k našemu repositáři, poté si zvolíme název našeho projektu, tento název bude použit i pro naší *.vercel.app doménu. Nakonec klikneme na tlačítko Deploy.

## Freenom doména

Pokud chceme zdarma doménu od Freenom, musíme přejít na [https://freenom.com](https://freenom.com) a do pole Find new FREE domain napíšeme (CoChceteJakoDomenu).tk. Pokud je dostupná tak jí můžeme až na 12 měsíců získat zdarma. Proto to udělejte, ověřte svůj email a dokončete nákup. Poté přejdeme na [https://my.freenom.com](https://my.freenom.com), přihlásíme se a vpravo nahoře klikneme na services a tam My domains. U naší domény klikneme na Manage domain. Klikneme na Managment tools a tam na nameservers. Zvolíme že chceme použít custom nameserver.

Do Nameserver 1 zadáme:

```
NS1.VERCEL-DNS.COM
```

A do Nameserver 2 zadáme:

```
NS2.VERCEL-DNS.COM
```

## Přidání domény do vercelu

Pro používání domény s naší NExt.js stránkou se přihlásíme se do Vercelu pomocí Githubu a zvolíme naší stránku. Dále klikneme na View Domains a do textového pole zadáme naši doménu, klikneme na Add a ve vyskakovacím okénku znovu klikneme na Add. Vercel nyní zkontroluje jestli používáme jejich name servery/DNS records. Pokud vám Vercel řekne, že máte špatnou konfiguraci, zkuste se znovu kouknout na Freenom a nebo prostě chvíli počkat. Dále už nám Vercel vygeneruje SSL certifikát pro naší doménu a máme hotovo! Náše stránka nyní používá naší doménu.

## Zakončení

Nyní již máme deploynutou naši stránku na Vercelu s naší vlastní doménou. Pár věcí si je ale třeba zapamatovat, vaše vercel stránka bude reflektovat to, co máte ve své main branch ve vašem github repu. Proto netestované commity doporučuji dávat na vedlejší branch, nebo jako já prostě jeďte YOLO a pushujte rovnou do main branch. Zároveň, Vercel bot který byl přidán do vašeho github repa bude u každého pullrequestu/pushe testovat vaší stránku a ukáže vám pokud se stránka buildne správně, tak na to dávejte pozor.

Díky za přečtení tohoto dlouhého blog postu, ✌️
