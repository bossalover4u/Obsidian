---
type: book
author:
  - Виктор Пелевин
titles: TRANSHUMANISM INC (Трансгуманизм Inc)
series:
cover: http://books.google.com/books/content?id=1O5YEAAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api
start: 2022-11-01
end: 2022-11-09
duration: 8
status: done
---
![cover|150](Resources/cover!150-15.jpg)

Автор: [[Щоденник прочитаного/Автори/Виктор Пелевин|Виктор Пелевин]]
Название: TRANSHUMANISM INC. (Трансгуманизм Inc.)
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
><p align="justify">В будущем богатые люди смогут отделить свой мозг от старящегося тела – и станут жить почти вечно в особом “баночном” измерении. Туда уйдут вожди, мировые олигархи и архитекторы миропорядка. Там будет возможно все.Но в банку пустят не каждого. На земле останется зеленая посткарбоновая цивилизация, уменьшенная до размеров обслуживающего персонала, и слуги-биороботы.Кто и как будет бороться за власть в этом архаично-футуристическом мире победившего матриархата? К чему будут стремиться очипованные люди? Какими станут межпоколенческие проблемы, когда для поколений перестанет хватать букв? И, самое главное, какой будет любовь?В связи с нравственным возрождением нашего общества в книге нет мата, но автору все равно удается сказать правду о самом главном.</p>
___

- [[home|У бібліотеку]]
```dataviewjs
const currentFront = dv.current().file.frontmatter; // Получаем название текущей заметки
const year = parseInt(currentFront['end'].split('-')[0]); // Преобразуем название заметки (год) в число
const yearLink = dv.fileLink(`Щоденник прочитаного/Списки прочитаних книг по роках/${year}`, false, `Що я прочитав за ${year} рік`);
dv.list([yearLink]);
```