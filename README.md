# 🎡 Zahlenkirmes — Zahlen & Mengen bis 10

Ein Lernspiel für den Schulanfang: Zahlen erkennen, Mengen erfassen und
Zahl mit Menge verbinden — auf einer freundlichen Kirmes mit sechs
verschiedenen Attraktionen. Bewusst **kein Rechenspiel**: Es kommen keine
Plus- oder Minusaufgaben vor.

**Zielgruppe:** Schuleingangsphase (Klasse 1, erste Wochen), später auch
Förderunterricht
**Status:** Version 1.0 — veröffentlichungsbereit

## 🎪 Die sechs Attraktionen

1. **Süßigkeitenstand** — Zahl → Menge herstellen: die passende Anzahl
   Bonbons in die Tüte packen (antippen, Auswahl korrigierbar)
2. **Entenangeln** — Ziffer → Menge erkennen: das Becken mit der
   richtigen Entenanzahl finden
3. **Ballonbude** — Menge → Ziffer: zu einer gezeigten Menge die
   passende Zahl wählen (plausible Nachbarzahlen als Distraktoren)
4. **Riesenrad** — Menge ergänzen: vorhandene Gondel-Plätze bis zur
   Zielzahl auffüllen (ohne dass irgendwo eine Plus-Aufgabe steht)
5. **Lichterblitz** — kurzes Zeigen eines Musters, dann verdeckt: „Wie
   viele hast du gesehen?" (altersgerechte Anzeigedauer, bei 6–10 immer
   strukturiert dargestellt)
6. **Zahlenkarussell** — mehrere Darstellungen derselben Zahl erkennen
   (Fingerbild, Würfelbild, Zehnerfeld, Punktemuster) — Mehrfachauswahl,
   Prüfung erst nach „Fertig"

Der Bereich (**Zahlen bis 5** oder **bis 10**) wird auf dem Startbildschirm
gewählt und gilt für alle sechs Minispiele gleichermaßen — auch für
falsche Antwortoptionen, damit im Modus „bis 5" nirgends eine Menge über 5
zu sehen ist.

Eine Runde besteht aus 8 richtig gelösten Aufgaben, sichtbar als
Kirmestickets 🎟️. Bei falschen Antworten gibt es keinen Punktabzug — die
Aufgabe bleibt bestehen, ein freundlicher Hinweis erscheint, das Kind
darf erneut versuchen.

## 🛠️ Technik

Eine einzige, in sich geschlossene `index.html`-Datei — kein Build-Prozess,
keine Abhängigkeiten, kein Server nötig.

- Reines HTML, CSS und JavaScript (kein Framework)
- **Sprachausgabe** über die native `SpeechSynthesis`-API (Deutsch),
  über einen Lautsprecher-Button bei jeder Aufgabe abrufbar; das Spiel
  funktioniert vollständig auch ohne verfügbare Sprachausgabe
- **Mathematisch korrekte Mengendarstellungen:** klassische Würfelbilder
  nur für 1–6 (keine erfundenen Muster für 7+), Fingerbilder mit
  5er-Struktur (eine Hand bis 5, zwei Hände ab 6), 2×5-Zehnerfeld mit
  konsistenter Füllreihenfolge, strukturierte 5+Rest-Darstellung für
  Zahlen über 5
- **Automatische Größenanpassung:** Bei mehreren Karten in einem Raster
  (z. B. beim Zahlenkarussell) wird die Grundgröße für alle Karten
  gemeinsam berechnet, nicht pro Karte einzeln — verhindert, dass
  einzelne Karten trotzdem über den verfügbaren Platz hinausragen,
  sobald sich die Zeilenhöhe eines CSS-Grids nach der größten Karte
  richtet
- Läuft vollständig offline, keine externen Ressourcen
- Responsiv für Smartboard, Desktop, Tablet und Smartphone
- Keine personenbezogenen Daten, keine Cookies, kein Tracking

## 📁 Projektstruktur

```
zahlenkirmes-projekt/
├── index.html      ← das komplette Spiel
├── README.md
└── .gitignore
```

## ▶️ Lokal ausprobieren

Einfach `index.html` im Browser öffnen — kein Server, keine Installation
nötig.

## 🌐 Veröffentlichung

### GitHub

1. Neues Repository auf [github.com](https://github.com) anlegen.
2. `index.html`, `README.md` und `.gitignore` hochladen.

### Netlify / Vercel

Reine statische HTML/CSS/JS-Seite ohne Build-Schritt — beide Plattformen
erkennen das automatisch, keine Konfiguration nötig.

**Netlify (per Drag & Drop, ganz ohne GitHub):**
1. Auf [app.netlify.com](https://app.netlify.com) einloggen.
2. Den Ordner mit der `index.html` direkt in den Browser ziehen
   („Deploy manually").
3. Netlify vergibt sofort einen Link.

**Vercel (über GitHub):**
1. Mit GitHub bei [vercel.com](https://vercel.com) einloggen.
2. „Add New…" → „Project" → Repository importieren → „Deploy".

## ✅ Qualitätssicherung

Vor der Freigabe automatisiert geprüft:

- **Drei kritische Fehler gefunden und behoben:**
  1. Alle Mengen-Darstellungen waren zunächst unsichtbar/verzerrt, da
     die CSS-Grundeinheit für die Größenberechnung ohne Standardwert
     definiert war.
  2. Bei der Ballonbude wurde die Größenanpassung aufgerufen, bevor das
     jeweilige Element im Dokument hing.
  3. Beim Riesenrad wurde die Figuren-Auswahl abgeschnitten, weil das
     Rad selbst nicht schrumpfen durfte — behoben durch eine
     konservativere Größenobergrenze.
- **Ein Regelverstoß behoben:** Im Modus „bis 5" konnten Distraktoren
  (falsche Antwortoptionen, falsche Karussell-Karten) noch Mengen von
  6–7 zeigen. Nach dem Fix: 0 Verstöße über 800 automatisiert generierte
  Stichproben in beiden Bereichen.
- **Zielzahl übersteigt niemals den gewählten Bereich** — geprüft über
  hunderte automatisiert generierte Aufgaben je Bereich
- Volle Runden (8/8) in beiden Bereichen, Bereich wechseln, Neustart mit
  korrektem Zurücksetzen des Fortschritts bei Beibehaltung des Bereichs
- Sprachausgabe verursacht keinen Fehler, wenn `SpeechSynthesis` im
  Browser nicht verfügbar ist
- Doppelklick/Doppeltipp vergibt kein doppeltes Ticket
- Zahlenkarussell: Prüfung erfolgt erst nach „Fertig", nicht bereits
  beim ersten Antippen; Mehrfachauswahl korrekt berücksichtigt
- Alle 6 vorgeschriebenen Bildschirmgrößen (375×667 bis 1920×1080)
  geprüft: kein horizontales Scrollen, keine abgeschnittenen Inhalte

## 📄 Lizenz

© Förderfreude Games. Alle Rechte vorbehalten.
