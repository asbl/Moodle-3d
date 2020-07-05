# IM³ Kursstruktur

IM³ ist ein Konzept wie Moodle-Kurse im Schulkontext gut umgesetzt werden können. 

Das Konzept wurde ursprünglich von [w_wobble](https://twitter.com/w_wobble) untem dem Namen "Merüf-Prinzip" und entwickelt. Eine Präsentation findet sich [hier](https://h5p.org/node/940193)

## Zentrale Ideen:

  * Stärkung des kollaborativen Austauschs
  * Einheitliche Struktur hilft Schülern bei der Orientierung in Moodle
  * Effizienter Austausch von Moodle-Materialien

## Aufbau

Das 3D-Modell ist auf 3 Ebenen aufgebaut:

![Struktur](https://i.imgur.com/F0xTrN9.png)


### Ebene 1: Klassenkurse

Auf Ebene 1 finden sich Klassenkurse. Hier finden sich alle Materialien für die **Klasse**, z.B. der Link zu einer Videokonferenz oder z.B. Materialien die in der Klasse eingesammelt werden.

Außerdem findet sich hier ein Link zu allen Fächern:

#### Beispiel

![Klassenkurs](https://i.imgur.com/ihXx9W9.png)
*Lizenz: CC BY 4.0 - von Andreas Siebel* - Die Icons wurden von Pascal Klenke gestaltet.

### Ebene 2: Fachkurse

Auf Ebene 2 finden sich die Fachkurse. Hier findet sich alles, was für die **Klasse** **und** das **Fach** von Bedeutung sind, z.B. aktuelle Abgaben und ein Link zum aktuellen Thema.

#### Beispiel

![Fachkurs](https://i.imgur.com/WJEeRNc.png)
*Lizenz: CC BY 4.0 - von Andreas Siebel*

### Ebene 3: Inhaltskurse

Auf Ebene 3 finden sich Inhaltskurse. Die Inhaltskurse sind Kurse zu bestimmten Themen in einem Fach, z.B. Lineare Funktionen, Prozentrechnung, […]

#### Beispiel

![Inhaltskurs](https://i.imgur.com/Pu5K2aL.png)
*Lizenz: CC BY 4.0 - von Andreas Siebel*


## FAQ

* **Warum brauche ich einzelne Inhaltskurse?**
  Dadurch, dass die Themen in einzelne Inhalte aufgespalten sind, können Lehrer gemeinsam Inhaltskurse bearbeiten. In ihren Fachkursen müssen sie dann jeweils nur einen Link zu dem entsprechenden Fachkurs setzen. Auf diese Art wird Teamarbeit gefördert.
* **Wofür brauche ich dann noch Fachkurse?**
  In Inhaltskursen können Schüler unterschiedlicher Klassen teilnehmen. Wenn es etwas gibt, dass in Klassen unterschiedlich gehandhabt wird (z.B. andere Abgabetermine für Hausaufgaben, Sprechstunden etc.), dann findet sich dies im Fachkurs.
* **Verliere ich da nicht die Freiheit individuell Sachen anders zu machen?**
  Nein. Du kannst Inhaltskurse verlinken. Du kannst diese aber auch klonen und an deine eigene Bedürfnisse anpassen. Du kannst Kurse auch ganz anders anlegen, wenn du dies möchtest. IM³ ist ein Baukasten.

## Varianten

  * Das Merüf-Prinzip: Das Merüf-Prinzip besteht aus **M**otivation, **E**rarbeitung, **R**egeln, **Ü**bungen, **F**ragen. Dies ist im usprünglichen Konzept der Grundaufbau von allen **Materialien in Inhaltskursen** und bietet auf diese Weise Schülern eine einheitliche Struktur. In dem Konzept von [w_wobble](https://twitter.com/w_wobble) enthält ein Inhaltskurs mehrere Bücher, die nach dem Prinzip MERÜF aufgebaut sind.

  * ENTWURF: An der CWS werden wir ein modifiziertes MERÜF-Prinzip verwenden: Angedacht ist, dass ein Kurs eine komplett abgeschlossene Einheit ist (1-2 Wochen Umfang) und aus einer festgelegten Phasenstruktur besteht. Im aktuellen Entwurf sind folgende Phasen vorgesehen: **M**otivation, **E**rarbeitung, **Überblick**, **A**nwenden, **Reflexion**, **Evaluation**. Die Begrifflichkeiten wurden leicht verändert um diese bessere in andere Fachbereiche zu übertragen. Möglicherweise gibt es aber auch mehrere Templates, aus denen Lehrer dann wählen können. Im Gegensatz zum Merüf-Prinzip enthält ein Kurs hier alle Phasen nur einmal, während in der Merüf-Variante mehrere Bücher in einem Kurs enthalten sind, die jeweils dieser Struktur folgen.

## Best Practices

  * **Die Kurse anlegen**: Klassenkurse und Fachkurse können per **csv-Datei** basierend auf einem Template angleegt werden. Auf diese Weise kann hier bereits eine einheitliche Struktur vorgegeben werden.

## Hilfreiche Module

Welche Module sind hilfreich, um das Konzept umzusetzen?

* **Subcourse**: Damit können Bewertungen aus Unterkursen in die Elternkurse übernommen werden. https://moodle.org/plugins/mod_subcourse

* **Course Templates**: Damit können Templates zur Erstellung von Inhaltskursen vorgegeben werden. https://moodle.org/plugins/local_course_templates

* **Filtered Course Lists**: Damit können Backlinks von den Inhaltskursen zu den oberen Ebenen realisiert werden. Hier können **Meine Fachkurse** oder **Meine Klassenkurse** angezeigt werden. Mit Javascript kann darüber auch der Breadcrumb überschrieben werden

Das Konzept ist unter CC0-Lizenz verfügbar, für Bilder gelten eigene Lizenzen: https://creativecommons.org/publicdomain/zero/1.0/deed.de

## Hacks

### Backlinks

  * Für den folgenden Hack müssen folgende Bedingungen gegeben sein:
  * Klassenkurse liegen im Kursbereich Klassenkurse.
  * Fachkurse liegen im Kursbereich Fachkurse.
  * Inhaltskurse liegen im Kursbereich Inhaltskurse.
  * In der Webseite-Administration ist die Einstellung "Meine Kursbereiche anzeigen" definiert
  * Auf der Kursseite wird ein Block "Meine Kurse" angezeigt

Mit folgendem Javascript können jetzt Backlinks im Breadcrumb erstellt werden, der Pfad wird entsprechend geändert. Füge dieses Javascript an irgendeiner Stelle mit <script></script>-Tags hinzu, in denen du Javascript verwenden darfst.

```javascript
$(window).on("load", function () {
  $("#page-navbar").each(function () {
    // Setze diese Variablen entsprechend
    var kursbereich_inhalte = 'Inhaltskurse'; // In welchem Kursbereich finden sich die Inhaltskurse?
    var kursbereich_faecher = 'Fachkurse'; // In welchem Kursbereich finden sich die Fachkurse?
    var kursbereich_klassen = 'Klassenkurse'; // In welchem Kursbereich finden sich die Inhaltskurse?

    function replace_breadcrumb(breadcrumb_text, type) {
      if ($("#page-navbar").is(':contains("' + breadcrumb_text + '")')) {
        if (type == "inhalt") {
          var breadcrumb_course = $(".breadcrumb-item:contains('" + breadcrumb_text + "')").next().text().trim();
          var cls_text = "Klasse " + $('.block_course_list li a:contains("' + breadcrumb_course + '")').text().split("-")[1].trim();
          var cls = $('.block_course_list li a:contains("' + cls_text + '")');
          var course = $('.block_course_list li a:contains("' + breadcrumb_course + '")');
          $(".breadcrumb-item:contains('" + breadcrumb_text + "')").each(function() {
            $(this).next().replaceWith(function () {
              course = course.wrap('<li class="breadcrumb-item"></li>').parent()
              return course;
            });
            $(this).replaceWith(function () {
              cls = cls.wrap('<li class="breadcrumb-item"></li>').parent()
              return cls;
            });
          });
        }
        else if (type == "fach") {
          var breadcrumb_class = "Klasse "+$(".breadcrumb-item:contains('" + breadcrumb_text + "')").next().text().split("-")[1].trim();
          var cls  = $('.block_course_list li a:contains("' + breadcrumb_class + '")');
          $(".breadcrumb-item:contains('" + breadcrumb_text + "')").replaceWith(function () {
            cls = cls.wrap('<li class="breadcrumb-item"></li>').parent()
            return cls;
          });
        }
      }
    }

    replace_breadcrumb(kursbereich_inhalte, "inhalt");
    replace_breadcrumb(kursbereich_faecher, "fach");

  });

});
```