---
type: book
author:
  - Кристофер Мур
titles: SACRÉ BLEU Комедия д’искусства
series:
cover: http://books.google.com/books/content?id=mmA2AgAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api
start: 2021-01-19
end: 2021-02-09
status: done
---
![cover|150](Кристофер%20Мур%20-%20SACRÉ%20BLEU%20Комедия%20д’искусства.jpg)

Автор:: [[Щоденник прочитаного/Автори/Кристофер Мур|Кристофер Мур]]
Название: SACRÉ BLEU. Комедия д’искусства
Серия:
Номер в серии:
Основные персонажи:

```dataviewjs
function daysBetween(startDate, endDate) {
	if (!startDate && !endDate) { 
		return "Укажите даты"; 
	} else if (startDate && !endDate) {
		return ("Читаю сейчас")
	}
	const oneDay = 24 * 60 * 60 * 1000; // hours * minutes * seconds * milliseconds
	const start = new Date(startDate);
	const end = new Date(endDate);
	const diffDays = Math.round(Math.abs((start - end) / oneDay));
	if (diffDays === 0) {
		return "Тот же день";   
	} else {
		let suffix;     
	    if (diffDays % 10 === 1 && diffDays % 100 !== 11) {
		    suffix = "день";     
	    } else if ([2, 3, 4].includes(diffDays % 10) && ![12, 13, 14].includes(diffDays % 100)) {
			suffix = "дня";     
		} else {       
			suffix = "дней";     
		}          
		return diffDays + " " + suffix;   
	} 
}  

const front = dv.current().file.frontmatter;
const start = front["start"]
const end = front["end"]
const data = [
  {start: start, end: end}
];

// Добавляем столбец "Продолжительность" с использованием функции daysBetween
const tableData = data.map(file => {
  const duration = daysBetween(start, end);
  return [start, end, duration];
});

dv.table(["Начал", "Закончил", "Продолжительность"], tableData);
```

***Інші книги автора***:
```dataviewjs
const currentFilename = dv.current().file.name;
const authors = dv.current().file.frontmatter['author'];

const folderpath = 'Щоденник прочитаного/Книги';

const books = app.vault.getFiles().filter(file =>
  file.path.includes(folderpath) &&
  file.basename !== currentFilename &&
  (Array.isArray(authors) ? authors.some(author => file.path.includes(author)) : file.path.includes(authors))
);

dv.list(books.map(file => dv.fileLink(file.path)));


```
***Інші книги серії:***
```dataviewjs
const front = dv.current().file.frontmatter;
if (front) {
	const series = front['series'];
	if (series) {
		const folderpath = 'Щоденник прочитаного/Книги';
		const currentFilename = dv.current().file.basename;
		const books = app.vault.getFiles().filter(file =>  
			file.path.includes(folderpath) && 
			dv.page(file.path)['series'] === series && 
			file.basename !== currentFilename &&
			file.path !== dv.current().file.path 
		);
		dv.list(books.map(file => dv.fileLink(file.path)));
	}
}

```

```dataviewjs
const front = dv.current().file.frontmatter;
if (front) {
	const series = front['series'];
	if (series) {
		const folderpath = 'Щоденник прочитаного/Книги';
		const currentFilename = dv.current().file.basename;
		const books = app.vault.getFiles().filter(file =>  
			file.path.includes(folderpath) && 
			dv.page(file.path)['series'] === series && 
			file.basename !== currentFilename &&
			file.path !== dv.current().file.path 
		);
		dv.list(books.map(file => dv.fileLink(file.path)));
	}
}

```

---
>[!info] Анотація
><p align="justify">«Я знаю, что вы сейчас думаете: «Ну, спасибо тебе огромное, Крис, теперь ты всем испортил еще и живопись» – так начинает Мур послесловие к этому роману. «Не испортил, а показал все совсем с другой стороны!» – непременно воскликнет благодарный читатель, только что перевернувший последнюю страницу романа про священную синь.Такого Мура мы еще не видели – насмешник и низвергатель авторитетов предстает перед нами человеком тонким и даже лиричным.А как иначе? Ведь в этой книге он пытается разгадать тайну творчества и рассказать о тех великих, которым удалось поймать мгновение и перенести его на холст.</p>

___

> [!quote] Цитата
> ***"Я вас умоляю, месье профессор, но я экспериментировал с абсентом и могу свидетельствовать о его опасных галлюциногенных свойствах. В особенности — о его способности превращать дурнушек в красавиц. — Ну, это восьмидесятиградусный спирт, а полынь в нем ядовита. Подозреваю, после приема у вас перед глазами мелькает ваша собственная смерть. — Да, но с изумительнейшим бюстом. Как вы это объясните?"***

>[!quote] Цитата
 ***"Наукой признано, что сам Господь наделил французов даром кухни. А когда спустился этажом ниже, проклял англичан тем же".***

*****
- [[home|В библиотеку]]
```dataviewjs
const currentFront = dv.current().file.frontmatter; // Получаем название текущей заметки
const year = parseInt(currentFront['end'].split('-')[0]); // Преобразуем название заметки (год) в число
const yearLink = dv.fileLink(`Щоденник прочитаного/Списки прочитаних книг по роках/${year}`, false, `Що я прочитав за ${year} рік`);
dv.list([yearLink]);
```