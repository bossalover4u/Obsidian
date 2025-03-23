---
type: book
author:
  - Терри Пратчетт
titles: Carpe Jugulum. Хватай за горло!
series: Ведьмы
cover: https://static.wikia.nocookie.net/discworld/images/a/a0/12098.jpg/revision/latest?cb=20210507151825&path-prefix=ru
start: 2021-06-21
end: 2021-06-27
status: done
---
![cover|150](Терри%20Пратчетт%20-%20Carpe%20Jugulum%20Хватай%20за%20горло!.jpg)

Автор:: [[Щоденник прочитаного/Автори/Терри Пратчетт|Терри Пратчетт]]
Название: Carpe Jugulum. Хватай за горло!
Серия:  `=this.series`
Номер в серии:  6
Основные персонажи: Веренс II, Матушка Ветровоск, Нянюшка Ягг, Маграт Чесногк, Агнесса Нитт, Грибо, Овес, Вампиры семейства Сорокула, Игорь, Агнесса Нитт

---
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

dv.table(["Начало", "Закончил", "Продолжительность"], tableData);
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

---
>[!info] Анотація
>_Они — [вампиры](https://discworld.fandom.com/ru/wiki/%D0%92%D0%B0%D0%BC%D0%BF%D0%B8%D1%80%D1%8B "Вампиры"), и это многое объясняет. Да, они спят в гробах, да, они питаются кровью, однако… все не так просто. Долой заскорузлые предания и предрассудки! Новый мир — новые повадки! Закаляйся святой водой! Религиозные символы — всего лишь картинки и предметы нательного украшения! Чеснок? Обычная приправа! Смело гляди в глаза наступающему дню! Они — новые вампиры. Они будут жить по-новому. И вы тоже будете жить по-новому. Вас заставят не бояться. Вас заставят снять с окон решётки. Вам будет хорошо. Люди и вампиры — братья навек._
>
> _А тех, кто не согласен, — «Карпе Югулум»!_

___
- [[home|До бібліотеки]]

```dataviewjs
const currentFront = dv.current().file.frontmatter; // Получаем данные текущей заметки 
const status = currentFront['status']; // Получаем статус книги 
const year_start = currentFront['start'] ? parseInt(currentFront['start'].split('-')[0]) : null; // Получаем год, если есть дата начала 
const year_end = currentFront['end'] ? parseInt(currentFront['end'].split('-')[0]) : null; // Получаем год, если есть дата окончания 
const yearLinkTitle = year_end ? `Що я прочитав за ${year_end} рік` : "Немає дати закінчення читання"; 
if (year_start === null &&  year_end === null) {
	dv.paragraph("<span style='background-color: red; color: black;'>Не вказані дати</span>")
}else if (status === "processing") { 
	dv.paragraph("<span style='background-color: purple;'>Книга читається зараз</span>");
} else if (year_end !== null) { 
	const yearLink = dv.fileLink(`Щоденник прочитаного/Списки прочитаних книг по роках/${year_end}`, false, yearLinkTitle); 
	dv.list([yearLink]); 
} else { 
	dv.paragraph(`<span style='background-color: red;'>${yearLinkTitle}</span>`);
}
```