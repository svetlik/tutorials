---
layout: default
title: Rails Girls приложение със Sinatra
permalink: sinatra-app-bg
---

# Уеб сайт с Ruby и Sinatra в Nitrous.io

*Базирано на [това ръководство](http://guides.railsgirls.com/sinatra-app/) от Piotr Szotkowski, [@chastell](https://twitter.com/chastell)*

Ръководството по-долу прави предположението, че имате регистрация в [Nitrous.io](https://nitrous.io).

## In HTML we trust - статичен сайт

HTML е основният градивен блок на сайтовете. Преди да се занимаем с това приложение, ще покрием основни понятия в HTML и CSS с помощта на вашия инструктор.

Създайте семпла страничка, която да играе ролята на ваша визитка, като следвате напътствията на инструктора. Може да видите [една примерна такава тук](http://railsgirls.hno3.org/dimitar). Знаете ли, че можете да разгледате HTML и CSS кода на всеки сайт? Питайте вашия инструктор как.

**Бонус ниво**, ако ви остане време тук, или в края на събитието. Направете си безплатен профил в [GitHub](https://github.com) и използвайте [това ръководство](https://pages.github.com/), за да публикувате току-що създадения си сайт-визитка онлайн, на безплатния хостинг на GitHub за статични страници. Ако потребителското ви име е radostina, то сайтът ви трябва да се намира на адрес [https://radostina.github.io](https://radostina.github.io).

## Динамичен сайт - за гласуване

След като сме се позабавлявали малко с HTML и CSS, е време да направим слеващата и важна стъпка – да напишем софтуер, който да създав HTML код вместо нас – и динамично.

Ще създадем малко приложение за гласуване. Ще го напишем от нулата с помощта на помощна библиотека за правене на уеб сайтове с Ruby, която се казва Sinatra. Sinatra е просто един от възможните инструменти, които можем да ползваме. Има и други, разбира се. Sinatra е сравнително компактна и семпла библиотека, която въпреки простотата си има много възможности.

Представете си, че планирате обяд с група приятели. Понякога изборът на място, от което максимално много хора да са доволни, е трудна задача. Програмистите обичаме да си създаваме инструменти, които да ни помагат с решаването на трудни задачи. Това ще е целта и на нашето приложение за гласуване.

> **Инструктор:**
>
> Обяснете накратко какво е [Sinatra](http://www.sinatrarb.com), какво е "библиотека"/"framework" и защо съществува това групиране на софтуер.

## Инсталиране на Sinatra

Първо се налага да инсталираме библиотеката Sinatra, която ще иползваме:

`gem install sinatra`

## Помощ (документация) за Sinatra

След като сме си инсталирали библиотеката, идва моментът да я използваме. По-долу ще ви даваме необходимия код, който да изпълните стъпка по стъпка, но ако някъде искате да се отклоните от примерите, или ударите на проблем, ще ви е необходима консултация с ръководството (документацията) на библиотеката Sinatra.

Тази документация се намира на адрес: <http://www.sinatrarb.com/intro.html>

Умението да се намира правилната документация и да се чете е много важно и често подценявано.

### Създайте своето първо Sinatra приложение

За да започнем нашето приложение, ще създадем една папка в Nitrous средата. Може да я кръстите както искате. Това може да стане както от дървото с папки и файлове, като кликнете с дясно копче върху "кореновата" папка `nitrous`, така и от терминала (конзолата), с командата `mkdir име_на_папката`. Попитайте инструктора си за обяснение за тези команди.

След като създадете папката, трябва да я направите "активна", като "влезете" в нея. В терминала това става с командата `cd име_на_папката` (съкращение от "change directory").

Когато сте в правилната директория, трябва да създадете един файл там. Отново може и от терминала, с `touch voter.rb`, и с дясно копче върху дървото с файлове. Файлът може да се казва `voter.rb` и да е със следното съдържание:

{% highlight ruby %}
require 'sinatra'

get '/' do
  'Здравей, гласоподавателю!'
end
{% endhighlight %}

В този Ruby файл ще се намира кодът (логиката) на вашето приложение. Можете да кръстите Ruby файла с каквото име желаете. `voter.rb` е просто примерно такова.

### Стартиране на приложението

От директорията, съдържаща създадения по-горе файл, изпълнете следната команда:

    ruby voter.rb -p 5000 -o 0.0.0.0

Ще видите да се появяват съобщения на екрана. След няколко секунди, приложението ви би трябвало да е заредило напълно и да е готово да обслужва потребители.

За да видите резултата, от менюто "Preview" изберете "Port 5000". В нов раздел на браузъра би трябвало да ви се отвори временен URL адрес, на който да видите текста "Здравей, гласоподавателю!". Ако там пише нещо друго, помолете инструктора си за помощ.

Забележка: Този URL, на който се зарежда вашето приложение, може да бъде зареден от всеки човек по света, но е временен и ще спре да е активен, ако си спрете приложението, или си затворите браузъра, излизайки от профила си в Nitrous.

За да правим промени по приложението, се налага да го спираме.

За да спрете приложението си, натиснете клавишната комбинация `ctrl-c`, когато фокусът ви е в терминала.

> **Инструктор:**
>
> Обяснете накратко, че кодът около `get` се грижи да посрещне заявките до `/` към нашето приложение и да върне отговор и че това, което пише вътре в низа, е това, което ще се покаже в браузъра на потребителя.
>
> Споменете накратко за `HTTP`, `GET`, `POST` и как информацията пътува между браузъра и сървъра (request -> response). По-долу ще стане въпрос отново за `GET` и `POST`.

### Добавяне на `index` страница

> **Инструктор:**
>
> Обяснете защо избираме точно името "index". Обяснете концепцията за шаблони (templates), още наричани "изгледи". Защо има нужда от това? Обяснете какво е ERB (embedded Ruby) и как става вмъкването на логика (Ruby) в изгледа и как HTML-ът се "динамизира". Споменете за това, че има и други начини за генериране на HTML от шаблони (например, [Slim](http://slim-lang.com/), [HAML](http://haml.info/) и други).

За да държим нещата подредени, ще направим папка, в която ще слагаме файловете на нашите "изгледи". Ще я кръстим "views" (логично, нали?)

Сложете следния код във файл, който се казва `index.erb` и се намира в папката `views`:

{% highlight erb %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8' />
    <title>Машина за гласуване</title>
    <link href='//netdna.bootstrapcdn.com/twitter-bootstrap/2.3.1/css/bootstrap-combined.min.css' rel='stylesheet' />
  </head>
  <body class='container'>
    <p>Къде да обядваме?</p>
    <form action='cast' method='post'>
      <ul class='unstyled'>
        <% CHOICES.each do |place_id, place_name| %>
          <li>
            <label class='radio'>
              <input type='radio' name='vote' value='<%= place_id %>' id='vote_<%= place_id %>' />
              <%= place_name %>
            </label>
          </li>
        <% end %>
      </ul>
      <button type='submit' class='btn btn-primary'>Гласувай!</button>
    </form>
  </body>
</html>
{% endhighlight %}

И добавете следния код във `voter.rb`:

{% highlight ruby %}
CHOICES = {
  'happy'        => 'Happy',
  'divaka'       => 'Дивака',
  'krivoto'      => 'Кривото',
  'ugo'          => 'Уго',
  'mr-pizza'     => 'Мистър Пица',
  'sun-moon'     => 'Слънце луна',
  'soul-kitchen' => 'Soul Kitchen',
}
{% endhighlight %}

Промете секцията с `get` действието така:

{% highlight ruby %}
get '/' do
  erb :index
end
{% endhighlight %}

Проверете дали всичко е наред, като пуснете отново вашето приложение с `ruby voter.rb -p 5000 -o 0.0.0.0`. Знаете ли, че в терминала имате история на последно изпълнените команди? Стрелките нагоре и надолу ви движат по тази история, когато в момента няма работеща команда там.

Очакваният резултат е списък с места за обяд, под формата на радио бутони и бутон "Гласувай!".

> **Инструктор:**
>
> Обяснете концепцията на типа данни "речник" (хеш). Обяснете защо HTML-ът, който сложихме в изгледа, се генерира от приложението ни (ако е нужно, покажете документацията на Sinatra, секцията за изгледи). Проверете в браузъра как изглежда вече генерирания HTML, за да се види разликата между шаблон и резултат.
>
> Обърнете внимание на цикъла с `each`. Обяснете откъде идват стойностите на променливите `place_id` и `place_name`.
>
> Ако е нужно, споменете, че `CHOICES` е константа и че това е необходимо, за да може да е с глобална видимост и да се "вижда" и в изгледа.

### Предаване на променливи към изгледите

Променете `index.erb` файла в папката `views`, за да добавите `<h1>…</h1>` тагове:

{% highlight erb %}
  <body class='container'>
    <h1><%= @title %></h1>
    <p>Къде да обядваме?</p>
{% endhighlight %}

Променете и `get` действието по следния начин:

{% highlight ruby %}
get '/' do
  @title = 'Добре дошли в машината за гласуване!'
  erb :index
end
{% endhighlight %}

> **Инструктор:**
>
> Споменете накратко, че `@title` е инстанционна променлива и че това е начин да се предават стойности (променливи) от "действието" (`get`) към шаблона на изгледа (`index.erb`). Формално, причината това да работи е, че в Sinatra и действието, и изгледите се оценяват в контекста на един и същи Ruby обект. Не е нужно да се говори за обекти и класове.

### Добавяне на възможност за изпращане на резултатите като POST

Добавете следното във `voter.rb`:

{% highlight ruby %}
post '/cast' do
  @title = 'Благодарим за вашия глас!'
  @vote  = params['vote']
  erb :cast
end
{% endhighlight %}

Създайте нов файл в папката с изгелди `views`, който се казва `cast.erb`. В него сложете следния HTML и ERB код:

{% highlight erb %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8' />
    <title>Машина за гласуване</title>
    <link href='//netdna.bootstrapcdn.com/twitter-bootstrap/2.3.1/css/bootstrap-combined.min.css' rel='stylesheet' />
  </head>
  <body class='container'>
    <h1><%= @title %></h1>
    <p>Вашият глас: <%= CHOICES[@vote] %></p>
    <p><a href='/results'>Вижте резултатите!</a></p>
  </body>
</html>
{% endhighlight %}

> **Инструктор:**
>
> Обяснете как работи `POST`. Откъде идват нещата в `params`? Как се съпоставят полетата във формуляра с нещата в `params`? Как можем да ги използваме? Защо изобщо има различни HTTP методи като GET (read-only) и POST (променя неща на сървъра)?

### Изнесете общия код в layout

Създайте файл `layout.erb` в папката с изгледите `views`. Сложете там следния код:

{% highlight erb %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8' />
    <title>Машина за гласуване</title>
    <link href='//netdna.bootstrapcdn.com/twitter-bootstrap/2.3.1/css/bootstrap-combined.min.css' rel='stylesheet' />
  </head>
  <body class='container'>
    <h1><%= @title %></h1>
    <%= yield %>
  </body>
</html>
{% endhighlight %}

След това махнете вече дублиращите се общи части с HTML от другите два шаблона (`index.erb` и `cast.erb`).

> **Инструктор:**
>
> Обяснете защо се прави тази операция. Разяснете, че другите изгледи се вмъкват на мястото на `yield` и не е нужно да носят информация за общия layout.

### Показване на резултатите

Paste the following code into `voter.rb`:

{% highlight ruby %}
get '/results' do
  @votes = { 'waw' => 7, 'krk' => 5 }
  erb :results
end
{% endhighlight %}

Create a new file in the `views` directory, called `results.erb`.

{% highlight erb %}
<table class='table table-hover table-striped'>
  <% CHOICES.each do |id, text| %>
    <tr>
      <th><%= text %></th>
      <td><%= @votes[id] || 0 %>
      <td><%= '#' * (@votes[id] || 0) %></td>
    </tr>
  <% end %>
</table>
<p><a href='/'>Cast more votes!</a></p>
{% endhighlight %}

Run `ruby voter.rb`, check
your results and quit the server with `ctrl-c`.

__COACH__: Explain HTML tables and how how the
missing values from the hash default to zero.



### Persist the results using YAML::Store

Time for something new! Let’s store our CHOICES.

Add the following to the top of `voter.rb`:

{% highlight ruby %}
require 'yaml/store'
{% endhighlight %}

Add some more code into `voter.rb` – replace
`post '/cast'` and `get '/results'` with the following:

{% highlight ruby %}
post '/cast' do
  @title = 'Thanks for casting your vote!'
  @vote  = params['vote']
  @store = YAML::Store.new 'votes.yml'
  @store.transaction do
    @store['votes'] ||= {}
    @store['votes'][@vote] ||= 0
    @store['votes'][@vote] += 1
  end
  erb :cast
end

get '/results' do
  @title = 'Results so far:'
  @store = YAML::Store.new 'votes.yml'
  @votes = @store.transaction { @store['votes'] }
  erb :results
end
{% endhighlight %}

__COACH__: Explain what YAML is.


### See how the YAML file changes when votes are cast

Let’s open `votes.yml`. And vote. And check again.

__COACH__: There will be situations when one or more students will
forget to quit the server before running it again. It’s a good
opportunity to search the Internet for a solution. They don’t
have to know everything about killing processes to find a solution.

__COACH__: In the end explain shortly the differences between Sinatra and Rails.

## Play with the app

Try to change things in the app in any way you see fit:

* Add some additional logic to the views.
* Redirect to the results outright.
* Add other votings; how would the YAML file need to change?
* Try to style the file in different ways.
