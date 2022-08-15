---
title: "Privátní Go Moduly"
date: 2022-08-03T16:16:36+02:00
draft: false
keywords:
- go
- golang
- moduly
- git
- build
categories:
- programming 
---

Klasická situace - mám nějakou soukromou knihovnu v go, kterou nemůžu nebo nechci ukázat světu. Přitom ji chci použít v nějakém svém projektu. Jak nastavit build v go, aby mi tento modul stáhl? Je to trochu větší práce než se na první dojem zdá...
<!--more-->

Jak asi víte, Go používá klasické verzovací systémy k distribuci svých komponent. Takže tu nefunguje nic jako npm, maven repository, Pip nebo snad cargo. Ono se to zná jako dobrý nápad, verze jsou buď tagy nebo commit hashe a vy tak nepotřebujete řešit publishing na nějaké další servery či služby.

Jenže ... 

Na pozadí go getu běží např. git, který klonuje cílové repozitáře a ty pak používá. Proto pokud používáte tento postup např. v CI/CD pipeline, potřebujete prostředí (docker image), který obsahuje git (nebo svn/mercurial).

Ve zkratce - tohle je postup, který mi pomohl : https://www.digitalocean.com/community/tutorials/how-to-use-a-private-go-module-in-your-own-project

Ano, musíte sáhnout hned do několika konfiguráků, nastavit env variables a pak nějak fungujete.

Ovšem pozor. **Pokud jste nikdy předtím gitem z domény repozitáře nic na svůj stroj netahali** , udělejte si nejdřív někam cvičný clone. Git se zeptá, jestli věříte novému klíči. Go get pod pokličkou na tomto totiž time-outuje. Prostě git visí a go get neví proč, tak chvíli čeká a pak zdechne. Na tomto jsem zabil nějakou tu hodinku, nemáte zač :)

PS: pokud máte to štěstí jako já a používáte GitLab se strukturou podskupin (subgroups), tak budete potřebovat ještě udělat jednu změnu do `go.mod`. Prostě přepíšete adresu repozitáře jako v tomhle příkladu: https://stackoverflow.com/a/70249074  

Ani očko nenasadíš, drahý Go vývojáři.

