# Tutorial de scrierea academică folosind Obsidian. Managementul referințelor bibliografice

Obsidian poate fi folosit împreună cu Zotero pentru a putea folosi Obsidian pentru editarea de lucrări științifice. Pornim de la premiza că în Zotero deja ai articolele de cercetare organizate.
## Conectarea lui Zotero cu Obsidian

Ca pas preliminar trebuie să ai deja instalat Zotero versiunea 6, unde ai deja colecția de înregistrări bibliografice aferentă articolului sau lucrării pe care o scrii.
### Instalarea plugin-urilor necesare în Zotero

Pentru a realiza un flux de lucru eficient folosind Zotero ca bază pentru înregistrările bibliografice și notele făcute pe fișierele PDF și Obsidian ca depozitar și instrument de analiză, bază de cunoaștere personală și editor de text, vom folos următoarele plugin-uri pe care le vom instala în Zotero:
• **Zotfile**: [http://zotfile.com/](http://zotfile.com/)  
• **BetterBibtex**: [https://retorque.re/zotero-better-bibtex/](https://retorque.re/zotero-better-bibtex/)  
• **Mdnotes**: [https://github.com/argenos/zotero-mdnotes/releases/tag/0.2.3](https://github.com/argenos/zotero-mdnotes/releases/tag/0.2.3)

**Zotfile** (http://zotfile.com/) este un manager avansat pentru PDF-urile atașate la înregistrările bibliografice din Zotero. O altă funcție foarte utilă este extragerea adnotărilor pe care le faci în fișierele PDF pentru că acest plugin permite crearea de adnotări și sublinieri direct pe textele fișierelor.
Pentru a instala Zotfile, trebuie să-l descarci de la Github, unde este dezvoltat acest plugin. Vei naviga la https://github.com/jlegewie/zotfile/releases de unde vei alege cel mai nou *release*, iar pentru acesta, derulând meniul de la butonul Assets, vei alege să descarci fișierul cu extensia `.xpi`.
Apoi, vei instala acest plugin din fișierul cu extensia `.xpi`. Având Zotero versiunea 6 deschis deja, mergi la meniul Tool -> Add-ons -> Tools for all Add-ons (rotița din colțul dreapta sus) -> Install Add-on From File unde vei alege pluginul.

**Better BibTeX** (BBT - https://retorque.re/zotero-better-bibtex/) este un plugin pentru a genera automat chei de citare pentru înregistrările bibliografice folosite într-o lucrare, dar mai mult de atât face conversii foarte utile între anumite formatări HTML ale lui Zotero în formule BibLaTex. Pentru a instala acest plugin, descarcă cea mai nouă versiune de la https://github.com/retorquere/zotero-better-bibtex/releases. Pentru a face puntea cu Obsidian, acest plugin este deosebit de important, fiind cel care asigură formatul corect al înregistrărilor bibliografice atunci când va trebui să exporți întreaga colecție. Mai jos vom detalia acest pas.

**Mdnotes** este un plugin care permite exportul notelor și al metadatelor create în Zotero, în format Markdown. Pentru mai multe detalii, accesați link-ul https://github.com/argenos/zotero-mdnotes. Pentru a-l instala, precum în cazul celorlalte două, se va accesa link-ul unde se găsesc versiunile care pot fi descărcate: https://github.com/argenos/zotero-mdnotes/releases.

**Instalarea pluginului Better Notes în Zotero**
Pentru a lucra și mai eficient cu adnotările pe care le faci pe un document, instalează și pluginul Better Notes. Pentru a avea un contact inițial cu scopul de a te pune la curent la ce este util, accesează https://github.com/windingwind/zotero-better-notes#readme. Unde se integrează fluxului nostru de lucru este menționat în următoarea secțiune a documentației: https://github.com/windingwind/zotero-better-notes#syncing-note-%EF%B8%8F-markdown. Folosind acest plugin poți ține notele din Obsidian sincronizate cu cele din Zotero.
Pentru a instala acest plugin, se va descărca de la https://github.com/windingwind/zotero-better-notes/releases fișierul cu extensia `.xpi` disponibilă accesând meniul Assets a ultimului release. Pentru instalare se vor repeta procedurile descrise mai sus în cazul celorlalte pluginuri pe care deja le-am instalat.

## Exportul datelor din Zotero într-un fișier live

Primul lucru care trebuie făcut este exportul unui fișier `.bib` din Zotero. Acest fișier trebuie să includă toate datele bibliografice ale articolelor și eventual alte cărților pe care le ai organizate folosind Zotero, fiind folosit de un plugin din Zotero denumit Citation. Cel mai bun lucru ar fi să exporți întreaga colecție din Zotero. Astfel, vei avea și un backup al înregistrărilor dincolo de realizarea punții cu Obsidian.

![[Export Better BibLaTex.png|600]]

Figura 1. Selectarea întregii biblioteci pentru a fi exportată ca fișier .bib

Pentru a face acest export necesar, mai întâi se va selecta *My Library*, apoi se va naviga pe meniul File ->Export Library iar din meniul de la Format se va opta pentru **Better BibLaTeX**. Se va bifa Export Notes, precum și Keep Updated, dar și Background export. Opțiunea Keep Updated este absolut necesară pentru ca de fiecare dată când se face o modificare în Zotero, aceasta să se reflecte și în fișierul care va fi rescris pe hard disk acolo unde ai ales să-l pui în structura de directoare proprie.
În cazul în care folosești mai multe computere, acest fișier ai putea să-l pui și pe un serviciu de găzduire cloud. Astfel, vei avea cea mai *proaspătă* versiune mereu.

Pentru a verifica setările necesare, vom merge în Zotero la Edit -> Preferences (shortcut: *CMD + ,*) -> Better BibTex -> Open Better BibTex Preferences... > Automatic Export

![[BibtexPreferences-AutomaticExport.png|800]]

Figura 2. Meniul Automatic Export din Preferințele plugin-ului Better BibTex

Din Figura 2 se observă faptul că toți pașii exportului au fost îndepliniți corect. Căile sunt specifice unui sistem Linux. Pentru fișierul de export, în acest caz s-a optat pentru denumirea de `Library-Zotero-all.bib`.
## Instalarea pluginului Citations

În Obsidian vom avea nevoie să instalăm pluginul Citation disponibil din Community Plugins al lui Obsidian. Câteva informații despre acest plugin se pot obține și de la https://github.com/hans/obsidian-citation-plugin. Acesta este pluginul care va citi fișierul pe care l-am creat în pasul anterior. În cazul exemplului ilustrat prin Figura 2, acesta se numește **Library-Zotero-all.bib**. 

Acum, vom proceda la configurarea plugin-ului din Setările Obsidian și alegând din coloana stângă sub Community plugins pe Citations. Apoi, în rădăcina vault-ului vom crea un subdirector în care vor fi aduse notele pe care le-ai făcut pe documentele PDF consultate în Zotero. Aceste texte ale adnotărilor pot fi transformate în note de Obsidian.

![[Citations-plugin-settings.png]]

Figura 3. Configurarea inițială a pluginului Citations

Ceea ce trebuie setat corespunzător este opțiunea de la *Citation database format*, unde se va alege BibLaTex (formatul ales pentru export anterior în Better Latex în Zotero). Apoi, la Citation database path se va pune calea întreagă până la fișierul live exportat din Zotero. În cazul unui sistem Linux, aceasta va fi similară cu următoarea: `/home/nicolaie/Documents/Library-Zotero-all.bib`. Ce mai trebuie făcut este să menționezi directorul în care vor fi create nodele aduse din Zotero. În cazul ilustrat de Figura 3, subdirectorul din *vault* desemnat ca destinație a notelor din Zotero în Obsidian este denumit `ZOTERO-NOTES`.

Mai departe, în setările acestui plugin de Obsidian, putem introduce un template (șablon) specializat pentru formatarea notei care va fi creată în *Literature note content template*. Un posibil șablon ar putea fi următorul.

```text
---
year: {{year}}
publisher: "{{publisher}}"
title: "{{title}}"
author: [{{authorString}}]
abstract: "{{abstract}}"
resources: ["{{DOI}}","{{URL}}"]
zotero: "{{citekey}}"
---
# {{title}}
{{authorString}}

{{abstract}}
```

Observă faptul că valorile câmpurilor pentru fiecare fragment de informație care va fi pus cap la cap în nota finală din Obsidian este menționat între acolade duble. În *template settings* sunt explicate câteva dintre valorile pe care le poți aduce din Zotero la momentul în care nota se construiește dinamic. În rest, nu este nimic special, ci numai markup-ul clasic al notei.
Adu-ți aminte de faptul că pentru a face sublinieri pe documentele PDF și pentru a crea note, ai nevoie de pluginul Mdnotes în Zotero.
Revenind la configurarea pluginului, dacă ai terminat cu propria combinație în ceea ce privește template-ul, poți să închizi și să te reîntorci la spațiu de lucru cu Obsidian-ul.

## Extragerea adnotărilor din Zotero

Să presupunem că în Zotero ai lucrat pe textul unui PDF care era atașament al unei înregistrări bibliografice dintr-o colecție. Mai jos în Figura 4, am făcut o captură de ecran a unei astfel de ipostaze. În documentul respectiv, am multe sublinieri care sunt importante pentru studiul unor politici europene privind datele de cercetare.

![[Ipostaza-de-lucru-cu-PDF-ca-atasament.png|800]]

Figura 4. Ipostază de lucru cu versiunea PDF a unui document atașat unei înregistrări din Zotero

După ce faci adnotările, va trebui să faci un pas suplimentar pentru a le integra ca parte componentă a înregistrării din Zotero.

![[ShowInLibrary-Zotero-cu-mdnotes.png|750]]

Figura 5. Întoarcere la notă cu Show in Library dând click drepta pe tabul în care lucrezi direct asupra PDF-ului

Așa cum este ilustrat în Figura 5, pentru a te reîntoarce la notă, vei da click dreapta pe tabul de editare al PDF-ului din a cărui meniu alegi Show in Library. 

![[Add note from Annotations.png|800]]

Figura 6. Adăugarea notelor făcute lucrând pe textul PDF-ului direct în înregistrare

După cum se vede în Figura 6 va trebui să dăm click dreapta pe înregistrarea din Zotero, de unde optezi pentru „Add Note from Annotations".

![[Vizualizarea adnotarilor cu Better Notes.png]]

Figura 7. Detaliile notelor afișate prin Better Notes

Privind mai atent la înregistrarea din Zotero, poți observa faptul că s-a adăugat o nouă componentă la înregistrare.

Având pluginul Better Notes deja instalat, dacă vei da click pe notele proaspete așa cum sunt înfățișate în Figura 7, în coloana din dreapta vor fi afișate toate sublinierile pe care le-ai făcut în timp ce ai studiat PFD-ul. Dacă nu ai pluginul Better Notes, vor fi afișate în coloana din drepta de instrumentul specific al lui Zotero.

Acest scenariu de lucru este îndeosebi foarte util atunci când lucrăm cu mai multe dispozitive. Dacă faci sublinieri și adnotări pe laptop, prin serviciul de sincronizare al Zotero, le vei avea disponibile și pe desktop ori pe tabletă.

## Sincronizarea Citations din Obsidian cu fișierul exportat din Zotero

După ce ai parcurs materialele dedicate studiului pentru a scrie un articol de cercetare, teză sau o notă care are nevoie de citări, vom trece în Obsidian pentru redactare.

Primul pas pe care îl vom face este să actualizăm baza de date cu referințe bibliografice generată de pluginul Citations. Pentru a face acest lucru, vom deschide panoul de comenzi (*Command Palette*), fie prin acționarea butonului din lista verticală din stânga (`>__`), fie apăsând combinația de taste **Ctrl (CMD pe Mac) + p**. Odată deschis panoul comenzilor, vom face o căutare începând să tastăm *Citations:*. Apar la vârf comenzile specifice pluginului Citations.

![[Citations Refresh Database.png|600]]

Figura 8. Deschiderea panoului de comenzi

Din cele patru comenzi care apar, vom alege *Citations: Refresh citation database* pentru a ne asigura că baza internă a pluginului este sincronizată cu fișierul proaspăt scris pe hard disk la momentul în care am adăugat adnotările. Adu-ți mereu aminte faptul că fișierul creat mai sus (în cazul acestui tutorial **Library-Zotero-all.bib**) este actualizat automat la fiecare cea mai mică modificare pe care o faci în Zotero. Aceste modificări trebuie să se reflecte și în propria evidență a pluginului Citations. Din acest motiv facem acest *Refresh citation database*.

În cazul în care dintr-un motiv arbitrar fișierul exportat pe disc nu include ultimele modificări făcute în Zotero, forțează exportul apăsând pe butonul *Export now* (Edit -> Preferences -> Better BibTex -> Open Better BibTeX prefferences... -> Automatic Export tab -> Export now). Apoi, în Obsidian refă pașii pentru a reîmprospăta Citations (comanda *Citations: Refresh citation database*).

## Instalare Pandoc și Obsidian Pandoc Reference List

După ce vei redacta documentul în Obsidian, vei dori să creezi un document final prin transformarea Markdown-ului în alte formate caracteristice unor editoare de text precum LibreOffice (.odt de la Writer) sau MS Office (.docx de la Word).
Pentru a face aceste transformări, vei avea nevoie de Pandoc. Instalează Pandoc pe propriul sistem de operare urmând instrucțiuni de la pagina acestui software: https://pandoc.org/installing.html.

Dacă ai instalat Pandoc, vei instala un instrument foarte util în Obsidian. Este vorba despre Obsidian Pandoc Reference List a cărui informații le poți consulta aici: https://github.com/mgmeyers/obsidian-pandoc-reference-list.

După ce ai instalat pluginul, mergi la opțiunile de configurare. Aici, primul lucru pe care trebuie să-l faci este să te asiguri că la calea către executabilul programului Pandoc este inserată corect calea. În figura de mai jos, în cazul unui sistem Linux/GNU Ubuntu avem o cale specifică.

![[Calea catre executabilul Pandoc.png|800]]

Figura 9. Verificarea căii unde este găsit executabilul programului Pandoc

Apoi, trebuie să trebuie să indici unde este fișierul acela live pe care îl salvează Zotero la orice modificare.

![[Calea catre fisierul cu bibliografia la zi.png|800]]

Figura 10. Calea către fișierul live pe care îl scrie Zotero prin Better LaTEx

După aceasta trebuie să-i precizăm pluginului ce stil de citare dorim să folosim în lucrarea/nota noastră. Pentru a face acest lucru, poți introduce câteva caractere în câmpul de la *Citation style* și din lista mare poți identifica cel care te interesează. Am ales Harvard, varianta adaptată de Universitatea Limerick (Cite It Right).

![[Alegerea stilului de citare.png|800]]

Figura 11. Alegerea stilului de citare.

În cazul în care dorești să precizezi stilul de citare folosind chiar un fișier CSL (https://citationstyles.org/) dedicat, mai întâi mergi și descarcă de la https://github.com/citation-style-language/styles stilul pe care îl dorești.

![[Fisierul pe Github de Harvard limerick.png|600]]

Figura 12. Căutarea și alegerea fișierului csl

Pentru a-l descărca, mai întâi dă un click pe el și din panoul următor alege „Download Raw File”.

![[Descarcarea CSL de pe Github.png|600]]

Figura 13. Descarcă fișierul csl (de fapt un fișier XML)

Având fișierul descărcat, poți să-l încarci de pe hard disk în câmpul de la *Custom citation style*.

![[Alegerea CSL-ului stilului de citare.png]]

Figura 14. Încărcarea fișierului CSL în plugin.
## Redactare cu Obsidian

Să presupunem că te-ai apucat să redactezi o notă în Obsidian și ai ajuns la punctul în care dorești să introduci o referință bibliografică. Pentru a face acest lucru, vei deschide din nou panoul comenzilor apăsând combinația de taste **Ctrl (CMD pe Mac) + p**. Vei începe să scrii la căutare Citations și din lista comenzilor care apar la vârf, vei alege Citations: Insert Markdown Citations. În panoul de căutare care va apărea, vei începe să scrii titlul lucrării pentru care vrei să creezi o referință bibliografică.

![[Cautare referinta bibliografica.png|800]]

Figura 15. Căutarea unei referințe bibliografice

Pentru a crea cel mai bun exemplu, vom crea mai jos o propoziție la care am să adaug o referință bibliografică.

Acesta este un fragment de text pentru exemplificare [@europeancommission.directorategeneralforresearchandinnovation.EOSCInteroperabilityFramework2021]

Ceea ce este observabil este următorul aspect. În Figura 15 de mai sus se observă o situație care induce confuzie. Sunt două înregistrări bibliografice ale aceleiași opere. Acest lucru se petrece pentru că în lucrul intensiv cu Zotero, în funcție de anumite situații, vei copia referințele bibliografice dintr-o colecție în alta sau chiar vei avea intrări duble sau mai multe pentru că ai uitat că ai mai introdus-o în altă parte. În cazul din Figura 9, înregistrarea de care am nevoie este cea care este subliniată vizual în captura de ecran. În schimb, ca reper general de lucru foarte important așa cum vezi în Figura 16 de mai jos, fiecare înregistrare bibliografică din Zotero are o cheie unică de identificare menționată în coloana din dreapta, tabul **Info** -> Citation Key. Acesta este elementul care va face diferența dintre înregistrările bibliografice, fiind și elementul în baza căruia poți face alegerea înregistrării corecte.

![[Alegerea referintei corecte.png|800]]

Figura 16. Informațiile privind înregistrarea bibliografică cu Citation Key care este un element de identificare unic.

Având instalat pluginul Obsidian Pandoc Reference List, referințele folosite în notă vor fi afișate dinamic în partea dreaptă.

![[Referintele in panoul din dreapta.png]]

Figura 17. Afișarea referințelor folosite în notă prin formatarea conform stilului de citare.