# CSS - upiększ to!

Nasz blog nadal wygląda dość surowo, prawda? Czas, aby to zmienić! Użyjemy do tego CSS.

## Czym jest CSS?

Kaskadowe arkusze stylów (ang. Cascading Style Sheets, CSS) to język używany do określania wyglądu i formatowania strony internetowej napisanej w języku znaczników (np. HTML). Traktuj go jak make-up dla naszej strony :).

Ale nie chcemy znów zaczynać od samego początku, prawda? Użyjemy, raz jeszcze, narzędzia uprzednio stworzonego przez programistów i opublikowanego przez nich w Internecie, za darmo. Nie ma sensu ponownie wynajdywać koła.

## Użyjmy biblioteki Bootstrap!

Bootstrap jest jednym z najpopularniejszych frameworków HTML i CSS do budowania pięknych stron: http://getbootstrap.com/

Został stworzony przez programistów, którzy pracowali dla Twitter-a i w chwili obecnej jest rozwijany przez ochotników z całego świata.

## Zainstaluj Bootstrapa

Aby zainstalować Bootstrap musisz dodać poniższe linijki do znacznika `<head>` w Twoim pliku `.html` (`blog/templates/blog/post_list.html`):

    html
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
    

Te linijki nie dodają żadnych plików do Twojego projektu. Wskazują one po prostu na pliki, które znajdują się w internecie. Otwórz teraz swoją przeglądarkę i odśwież stronę, a ujrzysz zmianę!

![Rysunek 14.1][1]

 [1]: images/bootstrap1.png

Od razu wygląda lepiej, prawda?

## Pliki statyczne w Django

Przyjrzymy się teraz bliżej temu co nazwałyśmy **plikami statycznymi**. Pliki statyczne to wszystkie pliki CSS i obrazki - pliki które nie są dynamiczne, czyli ich zawartość nie zależy od treści zapytania i dla każdego użytkownika są identyczne.

### Gdzie umieścić pliki statyczne w Django

Tak jak widziałaś wcześniej, gdy odpaliliśmy komendę `collectstatic` na serwerze, Django już wiedziało gdzie znaleźć pliki statyczne potrzebne do wbudowanej apki admina. Teraz chcemy dodać pliki statyczne do naszej aplikacji `blog`.

Wystarczy, że w naszej aplikacji stworzymy nowy folder i nazwiemy go `static`:

    djangogirls
    ├── blog
    │   ├── migrations
    │   └── static
    └── mysite
    

Django automatycznie znajdzie każdy folder nazwany "static" w każdej z twoich aplikacji i będzie mógł użyć plików statycznych tam się znajdujących.

## Twój pierwszy arkusz CSS!

Stwórzmy teraz arkusz CSS, aby dodać do Twojej strony Twój własny styl. Stwórz katalog o nazwie `css` w środku folderu `static`. Następnie utwórz nowy plik o nazwie `blog.css` w katalogu `css`. Gotowa?

    djangogirls
    └─── blog
         └─── static
              └─── css
                   └─── blog.css
    

Czas, by napisać trochę styli CSS! Otwórz `blog/static/css/blog.css` w Twoim edytorze kodu.

Nie będziemy się zanadto zagłębiać w style, ani uczyć się o arkuszach CSS, bo jest to całkiem łatwe i możesz nauczyć się tego samodzielnie po tym warsztacie. Naprawdę polecamy wziąć udział w [kursie Codeacademy HTML & CSS][2], by nauczyć się wszystkiego czego potrzebujesz o robieniu ładniejszych stron internetowych.

 [2]: http://www.codecademy.com/tracks/web

Jednak zróbmy chociaż trochę. Może moglibyśmy zmienić kolor naszego nagłówka? Do rozpoznawania kolorów komputery używają specjalnych kodów. Kody te zaczynają się od znaku `#`, po którym następuje 6 znaków. Każdy znak to cyfra (0-9) lub litera (A-F). Możesz znaleźć kody kolorów na przykład tutaj: <http://www.colorpicker.com/>. Możesz również użyć uprzednio [zdefiniowanych kolorów][3], takich jak `red` (czerwony) czy `green ` (zielony)..

 [3]: http://www.w3schools.com/cssref/css_colornames.asp

Do `blog/static/css/blog.css` powinnaś dodać następujący kod:

    css
    h1 a {
        color: #FCA205;
    }
    

`h1` to selektor CSS. To oznacza, że nadajemy style do każdego elementu `a` znajdującego się w elemencie `h1` (np. kiedy w kodzie mamy coś takiego: `<h1><a href="">link</a></h1>`). W tym przypadku nadajemy mu kolor `#FCA205`, czyli pomarańczowy. Oczywiście kolor jest dowolny!

W pliku CSS ustalamy styl dla elementów znajdujących się w pliku HTML. Elementy HTML identyfikujemy przez nazwę (n.p. `a`, `h1`, `body`), atrybut `class` lub atrybut `id`. Nazwę klasy lub id ustalasz sama dowolnie. Ta sama nazwa klasy może być przypisana do wielu elementów, ale id musi być unikalne dla całego kodu HTML. Przykładowo następujący tag możemy zidetyfikować w CSS używając nazwy `a`, klasy `external_link` lub id `link_to_wiki_page`:

    html
    <a href="http://en.wikipedia.org/wiki/Django" class="external_link" id="link_to_wiki_page">
    

O selektorach CSS możesz przeczytać więcej tutaj: [CSS Selectors in w3schools][4].

 [4]: http://www.w3schools.com/cssref/css_selectors.asp

Następnie musimy powiedzieć naszemu szablonowi HTML, że dodaliśmy nowe style CSS. Otwórz plik `blog/templates/blog/post_list.html` i dodaj tę linijkę na samym jego początku:

    html
    {% load staticfiles %}
    

Tym sposobem HTML załaduje nasze style CSS :) Następnie, pomiędzy `<head>` i `</head>`, zaraz za linkami do Boostrapa, dodaj poniższą linijkę. Przeglądarka czyta pliki w kolejności w której je wpiszesz, dzięki temu możemy nadpisać niektóre style Bootstrapa.

    html
    <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    

Właśnie pokazaliśmy naszemu szablonowi gdzie znajduje się nasz plik CSS.

Twój plik powinien teraz wyglądać tak:

    html
    {% load staticfiles %}
    <html>
        <head>
            <title>Django Girls blog</title>
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
            <link rel="stylesheet" href="{% static 'css/blog.css' %}">
        </head>
        <body>
            <div>
                <h1><a href="/">Django Girls Blog</a></h1>
            </div>
    
            {% for post in posts %}
                <div>
                    <p>published: {{ post.published_date }}</p>
                    <h1><a href="">{{ post.title }}</a></h1>
                    <p>{{ post.text|linebreaks }}</p>
                </div>
            {% endfor %}
        </body>
    </html>
    

Ok, teraz zapisz plik i odśwież stronę!

![Rysunek 14.2][5]

 [5]: images/color2.png

Super! Niezła robota. Może damy teraz naszej stronie trochę przestrzeni i zwiększymy margines po lewej stronie? Spróbujmy!

    css
    body {
        padding-left: 15px;
    }
    

Dodaj powyższy CSS do twojego pliku, zapisz go i sprawdź jak zadziałał!

![Rysunek 14.3][6]

 [6]: images/margin2.png

Może zmienimy też rodzaj czcionki w naszym nagłówku? Wklej to do sekcji `<head>` w pliku `blog/templates/blog/post_list.html`:

    html
    <link href="http://fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css">
    

Ta linia zaimportuje czcionkę zwaną *Lobster*, jedną z czcionek Google (<https://www.google.com/fonts>)

Dodaj linijkę `font-family: 'Lobster';` do pliku CSS `blog/static/css/blog.css` w środku znacznika `h1 a` (między nawiasami `{` i `}`) i odśwież stronę:

    css
    h1 a {
        color: #FCA205;
        font-family: 'Lobster';
    }
    

![Rysunek 14.3][7]

 [7]: images/font.png

Wspaniale!

Jak wspomniałyśmy wcześniej, kaskadowe arkusze stylów używają pojęcia klasy, które pozwala Ci wyodrębnić fragment kodu HTML i zastosować dane style tylko do niego, nie zmianiając wyglądu pozostałych części strony. To super przydatna opcja w przypadku gdy posiadasz dwa `div`y które robią zupełnie inne rzeczy (np. nagłówek i div zawierający post), więc nie chcesz, żeby wyglądały one tak samo.

Śmiało! Nazwijmy kilka części Twojego kodu HTML. Dodaj klasę nazwaną `page-header` do Twojego `div` który zawiera nagłówek:

    html
    <div class="page-header">
        <h1><a href="/">Django Girls Blog</a></h1>
    </div>
    

Teraz dodaj klasę `post` do Twojego `div` zawierającego post bloga:

    html
    <div class="post">
        <p>published: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaks }}</p>
    </div>
    

A teraz dodamy bloki deklaracji do selektorów. Selektory zaczynające się od `.` odnoszą się do klas. W internecie dostępnych jest mnóstwo świetnych samouczków i instrukcji poświęconych CSS, dzięki którym łatwiej będzie Ci zrozumieć poniższy kod. Na razie po prostu skopiuj i wklej do `blog/static/css/blog.css` poniższy kod:

    css
    .page-header {
        background-color: #ff9400;
        margin-top: 0;
        padding: 20px 20px 20px 40px;
    }
    
    .page-header h1, .page-header h1 a, .page-header h1 a:visited, .page-header h1 a:active {
        color: #ffffff;
        font-size: 36pt;
        text-decoration: none;
    }
    
    .content {
        margin-left: 40px;
    }
    
    h1, h2, h3, h4 {
        font-family: 'Lobster', cursive;
    }
    
    .date {
        float: right;
        color: #828282;
    }
    
    .save {
        float: right;
    }
    
    .post-form textarea, .post-form input {
        width: 100%;
    }
    
    .top-menu, .top-menu:hover, .top-menu:visited {
        color: #ffffff;
        float: right;
        font-size: 26pt;
        margin-right: 20px;
    }
    
    .post {
        margin-bottom: 70px;
    }
    
    .post h1 a, .post h1 a:visited {
        color: #000000;
    }
    

Teraz otocz kod HTML wyświetlający posty deklaracjami klas. Zamień to:

    html
    {% for post in posts %}
        <div class="post">
            <p>published: {{ post.published_date }}</p>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaks }}</p>
        </div>
    {% endfor %}
    

w pliku `blog/templates/blog/post_list.html` na to:

    html
    <div class="content container">
        <div class="row">
            <div class="col-md-8">
                {% for post in posts %}
                    <div class="post">
                        <div class="date">
                            {{ post.published_date }}
                        </div>
                        <h1><a href="">{{ post.title }}</a></h1>
                        <p>{{ post.text|linebreaks }}</p>
                    </div>
                {% endfor %}
            </div>
        </div>
    </div>
    

Zapisz te pliki i odśwież swoją stronę.

![Rysunek 14.4][8]

 [8]: images/final.png

Woohoo! Wygląda super, prawda? Kod, który właśnie wkleiliśmy nie jest zbyt trudny, więc zapewne orientujesz się, o co w nim chodzi.

Nie bój się pomajstrować trochę przy CSS, pozmieniać niektóre rzeczy. Jeżeli coś zepsujesz – nie martw się, zawsze możesz cofnąć!

Tak czy owak, warto zrobić darmowy kurs CSS & HTML na [Codecademy][2] w ramach “powarsztatowej pracy domowej”, żeby dowiedzieć się wszystkiego czego potrzebujesz do upiększania swoich stron przy użyciu CSS.

Gotowa na następny rozdział?! :)