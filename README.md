
<html>
<head>
  
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>MultiLingual</title>
    <style>
        button {
            font-size: 30px;
            padding: 0.25 2rem;
            margin: 1rem;
            width: 10rem;
            cursor: pointer;
        }

        [lang="en-CA"] {
            border: 5px solid #dd0000;
            margin: 1rem;
        }

        [lang="fr-CA"] {
            border: 5px solid limegreen;
            margin: 1rem;
        }

        [lang="de"] {
            border: 5px solid gold;
            margin: 1rem;
        }

        div[lang] {
            display: none;
        }

        div[lang].lang-match {
            /* background-color: cornflowerblue; */
            display: block;
        }
    </style>
</head>
<body>

<h1>Remove plagirism from text</h1>
<p>Enter text to remove plag.</p>
  <form action="/action_page">
  <textarea name="message" rows="20" cols="50"></textarea>
  <br><br>
  <input type="submit">
</form>

    <div lang="en-CA">
        <button data-key="btn-yes">Actual</button>
        <button data-key="btn-no">Actual</button>
    </div>
    <div lang="de">
        <button data-key="btn-yes">DEFAULT</button>
        <button data-key="btn-no">DEFAULT</button>
    </div>
    <div lang="fr-CA">
        <button data-key="btn-yes">DEFAULT</button>
        <button data-key="btn-no">DEFAULT</button>
    </div>

    <script>
        //language data... could come from an external js/json file
        let langdata = {
            "languages": {
                "en": {
                    "strings": {
                        "btn-yes": "yes",
                        "btn-no": "no"
                    }
                },
                "fr": {
                    "strings": {
                        "btn-yes": "oui",
                        "btn-no": "non"
                    }
                },
                "de": {
                    "strings": {
                        "btn-yes": "ja",
                        "btn-no": "nein"
                    }
                }
            }
        }
    </script>
    <script>
        //apply the language values to the content
        document.addEventListener('DOMContentLoaded', () => {
            //skip the lang value in the HTML tag for this example
            let zones = document.querySelectorAll('html [lang]');
            applyStrings(zones);

            let lang = findLocaleMatch();
            let container = document.querySelector(`html [lang*=${lang}]`);
            container.className = 'lang-match';
        });

        function applyStrings(containers) {
            containers.forEach(container => {
                //find all the elements that have data-key
                let locale = container.getAttribute('lang');
                //console.log('looking inside of ', locale);
                container.querySelectorAll(`[data-key]`).forEach(element => {
                    let key = element.getAttribute('data-key');
                    //console.log(element);
                    //console.log(key);
                    let lang = locale.substr(0, 2); //first 2 characters
                    if (key) {
                        element.textContent = langdata.languages[lang].strings[key];
                    }
                });
            })
        }

        function findLocaleMatch() {
            let keys = Object.keys(langdata.languages); //from our data
            let locales = Intl.getCanonicalLocales(keys); //from our data validated

            let lang = navigator.language; //from browser 
            let locale = Intl.getCanonicalLocales(lang); //from browser validated
            console.log('browser language', lang);
            console.log('locales from data file', locale);

            //find the match for locale inside locales
            let langMatch = document.documentElement.getAttribute('lang'); //default
            locales = locales.filter(l => locale == l);
            langMatch = (locales.length > 0) ? locales[0] : langMatch;
            return langMatch;
        }
    </script>

  
  
  
  
  

</body>
</html>
