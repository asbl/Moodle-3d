# IM³ - Technik

## Hilfreiche Module

Welche Module sind hilfreich, um das Konzept umzusetzen?

* **Subcourse**: Damit können Bewertungen aus Unterkursen in die Elternkurse übernommen werden. https://moodle.org/plugins/mod_subcourse

* **Course Templates**: Damit können Templates zur Erstellung von Inhaltskursen vorgegeben werden. https://moodle.org/plugins/local_course_templates

* **Filtered Course Lists**: Damit können Backlinks von den Inhaltskursen zu den oberen Ebenen realisiert werden. Hier können **Meine Fachkurse** oder **Meine Klassenkurse** angezeigt werden. Mit Javascript kann darüber auch der Breadcrumb überschrieben werden

Das Konzept ist unter CC0-Lizenz verfügbar, für Bilder gelten eigene Lizenzen: https://creativecommons.org/publicdomain/zero/1.0/deed.de

## Hacks

### Backlinks

  * Für den folgenden Hack müssen folgende Bedingungen gegeben sein:
  * Klassenkurse liegen im Kursbereich Klassenkurse. Sie haben die Struktur: #Klasse 5C, #Klasse 6C 
  * Fachkurse liegen im Kursbereich Fachkurse und haben die Struktur: #Fach - Klasse - Kürzel (z.B. #Deutsch - 5A - Si oder #Mathe - 6a - Si)
  * Inhaltskurse liegen im Kursbereich Inhaltskurse. Sie haben eine beliebige Struktur, dürfen aber nicht mit einem Hashtag beginnen)
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
          var course_search_text = "#" + $(".breadcrumb-item:contains('" + breadcrumb_text + "')").next().text().trim();
          var course = $('.block_course_list li a:contains("' + course_search_text + '")');
          $(".breadcrumb-item:contains('" + breadcrumb_text + "')").each(function() {
            $(this).next().replaceWith(function () {
              course = course.wrap('<li class="breadcrumb-item"></li>').parent()
              return course;
            });
            $(this).replaceWith(function () {
              var cls_search_text = "#Klasse " + $(this).next().text().split("-")[1].trim();
              var cls = $('.block_course_list li a:contains("' + cls_search_text + '")');
              cls = cls.wrap('<li class="breadcrumb-item"></li>').parent()
              return cls;
            });
          });
        }
        else if (type == "fach") {
          var breadcrumb_class = "#Klasse "+$(".breadcrumb-item:contains('" + breadcrumb_text + "')").next().text().split("-")[1].trim();
          var cls  = $('.block_course_list li a:contains("' + breadcrumb_class + '")');
          $(".breadcrumb-item:contains('" + breadcrumb_text + "')").replaceWith(function () {
            cls = cls.wrap('<li class="breadcrumb-item"></li>').parent()
            return cls;
          });
        }
        else if (type == "klasse") {
          $(".breadcrumb-item:contains('" + breadcrumb_text + "')").replaceWith(function () {
            return "";
          });
        }
      }
    }

    replace_breadcrumb(kursbereich_inhalte, "inhalt");
    replace_breadcrumb(kursbereich_faecher, "fach");
    replace_breadcrumb(kursbereich_klassen, "klasse");

  });

});
```