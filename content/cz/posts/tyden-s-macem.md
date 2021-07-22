---
title: "Týden s Macem 1 - Železo"
date: 2021-07-15T14:13:35+02:00
draft: true
---

Ano, je to tak. S novým začátkem v nové práci jsem se rozhodl změnit svoji vývojovou platformu. Co bylo hlavním lákadlem? Přiznám se, že jsem chtěl hlavně zjistit, jak si vede nová ARM-based architektura M1 a jestli je dobrá pro řadového developera k vývoji. A nakonec jsem toho objevil mnohem více...

A tak volba padla na třinácti-palcový MacBook Air M1. 

TL;DR: "Ten hardware je perfektní, ale s tím systémem budeš ze začátku fakt bojovat".

Vzhledově vypadá hezky a bytelně. Tužší otevírání víka nemusí sedět každému, ale dává to pocit bytelnosti. Nemožnost rozevřít notebook na 180 stupňů může být pro někoho limitujícím prvkem, ale mě to nijak žíly netrhá.
Displej je sice lesklý, ale s krásným a jemným rozlišením.

Pak tu máme hezky velký trackpad s opravdu pohodlnou klávesnicí. Jakože fakt, už jsem dlouho neviděl tak příjemnou klávesnici na psaní. Tím tedy myslím na poměry notebooků - není to žádný mechanický CherryMX. Na jednom boku je překvapivě 3,5" jack pro sluchátka, na tom druhém dva USB-C konektory.

U těch USBček se zastavím. Ano, vypadá to, že je jich málo. Ano, víc konektorů je vždycky lepší než méně. Ano, občas se u sebe hodí mít USB-hub.

Ale v práci to neřeším. Prostě vezmu USB-C kabel, který z NB vyvedu do monitoru, ve kterém mám zapojenou klávesnici a myš a který se tak chová jako displej a docking station najednou. Dokonce zvládá notebook i napájet, takže nemusím tahat druhý napájecí kabel. Krásná práce.

Co ještě musím zmínit (a v dnešní telco době docela důležitý faktor) je výborný integrovaný mikrofon. Stačí mít stroj položený na stole a chodit po místnosti a druhá strana mě v pohodě slyší. Opět kvalitní kus hardwaru.

Celý tenhle stroj je bez aktivního chlazení, je to čistý pasiv. Takže tohle vám prostě nebude nikdy hučet, protože v něm nemá co hučet.

No a teď ten hlavní zázrak - procesor.

Je to tedy applovská M1 - založená na 64bitovém ARMu. Má to 8 jader, půlka jich je "na výkon", druhá "na výdrž". Nic co bychom neznali z mobilního světa. Celý to dokáže tikat na 3,2 GHz.  Má to v sobě i nějaký GPUčko, jasně nečekejte žádný herní trhač asfaltu, ale svoji funkci udělá.

Výkon je ale pro řadového developera plně dostačující. Nemám problém, že by mi kompilace (java/go) vytížila zdroje natolik, že by byl jinak nepoužitelný nebo že by trvala nějak neúnosně dlouho.
Faktem je, že mám verzi s 16GB RAM, což je velmi příjemné (ale popravdě by možná i ta 8ka stačila)

Co to žere? V klidu pod 10W, když ho vytočíte tak něco přes třicet. Takže na napájení vám fakt stačí lepší nabíječka od mobilu. A hlavně to vydrží přes den nabitý. Přes den nemyslím 8 hodin pracovní doby, pohybujeme se zrovna kolem dvojnásobku. A to je moc příjemné.

No, ale co se na tom dá spustit? Vlastně (skoro) všecko. Hodně vývojářů softwaru pro jablka už svoje programy naportovalo i pro tuto platformu. To platí i vývojářských nástrojích - gradle, terraform a další už mají nativní podporu pro Arm64. Všechno ostatní se dá pustit přes emulaci Rosetta2. Takže se vám nestane, že by vám software, který vám doteď fungoval najednou fungovat přestal. S jednou výjimkou.

A tou je virtualizace. Protože hypervisor jde víc do hloubky, co se architektury týče, takže pokud pracujete s x86 virtuálkami, **budete mít problém**. Aspoň tedy aktuálně.

K problému - virtualizace znamená, že pustíte x86 virtuální systém na x86 procesoru. Nebo ARM systém na ARM procesoru. A asi už tušíte kde je problém.

Toto se dá řešit emulací - tzn ARM procák předstírá, že je ve skutečnosti x86 a že pro něj x86ka není žádný problém. Ale to prostě stojí část výkonu, protože každý předstírání něčeho je záhul.

Situace se má tak, že Parallels nějak fungují - ale x86 Windows na nich nepustíte. Ano, najdete na stránkách, že Win podporují, ale jen jejich ARMovou verzi, která se běžně neprodává (a na kterých ne všechny x86 programy fungují). Tak pozor na to. VMWare na podpoře M1ky pracuje, na podzim snad bude jasněji, co všechno budou podporovat. Ale obecně bych na podporu x86 WIN moc nesázel. Komunita z VirtualBoxu podporu M1 odpískala, zdá se, úplně.

Záchranou může být [UTM](https://mac.getutm.app), který je takový hezký frontend nad QEMU - takže vám to nějaký trn z paty vytrhne, ale je to po-ma-lý. Protože to není virtualizace ale pouze emulace. A navíc stálě poměrně nestabilní. Ale jako nouzovka dobrý.

Takže ano. Všechno má své stinné stránky a přechod na novou platformu rozhodně není bezbolestný. Nezbývá než věřit, že se situace do budoucna zlepší a optimismus by měl být na místě, protože Apple s prosazováním svých chipsetů to očividně myslí velmi vážně.

A další pozitivní tečka na závěr - 27. června 2021 v kernelu Linuxu (ve verzi 5.13) přibyla první vlaštovka podpory M1 chipsetu. Takže pokud bojujete se systémem jako já, je to taky dobrá zpráva. Ale o tom až příště!

