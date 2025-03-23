---
type: book
author:
  - Володимир В'ятрович
titles: Iсторія з грифом "Секретно"
series:
cover: https://bit.ly/3O3Eppk
start: 2024-01-17
end: 2024-01-19
status: done
---
![cover|150](media/cover!150-349.jpg)

Автор:: [[Щоденник прочитаного/Автори/Володимир В'ятрович|Володимир В'ятрович]]
Назва: Iсторія з грифом "Секретно"
Серія:  `=this.series`
Номер в серії:
Основні персонажі:

---
```dataviewjs
function daysBetween(startDate, endDate) {
	if (!startDate && !endDate) { 
		return "Вкажіть дати"; 
	} else if (startDate && !endDate) {
		return ("Читаю зараз")
	}
	const oneDay = 24 * 60 * 60 * 1000; // hours * minutes * seconds * milliseconds
	const start = new Date(startDate);
	const end = new Date(endDate);
	const diffDays = Math.round(Math.abs((start - end) / oneDay));
	if (diffDays === 0) {
		return "Той же день";   
	} else {
		let suffix;     
	    if (diffDays % 10 === 1 && diffDays % 100 !== 11) {
		    suffix = "день";     
	    } else if ([2, 3, 4].includes(diffDays % 10) && ![12, 13, 14].includes(diffDays % 100)) {
			suffix = "дня";     
		} else {       
			suffix = "днів";     
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

dv.table(["Почав", "Закінчив", "Тривалість"], tableData);
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
>Володимир В’ятрович — кандидат історичних наук, дослідник історії українського визвольного руху, директор Українського інституту національної пам’яті, автор багатьох книжок, присвячених історії України ХХ століття. Лауреат премії імені Василя Стуса — 2012 за розкриття таємниць архівів радянських спецслужб від ЧК до КҐБ та актуальну публіцистичну працю «Історія з грифом “Секретно”».
>Ця книга — зустріч із минулим. Тут — 61 історія, 73 роки і величезна кількість людей, котрі дивляться на читача зі світлин та архівних документів. Разом вони складають образ українського ХХ століття — часу, коли світ по-справжньому відкрив для себе Україну та українців, століття, коли творилося обличчя України. Сьогодні Володимир В’ятрович розповідає про минуле України 1918—1991 років. Описані в сухих звітах і відтворені сьогодні істориком хитрі спецоперації, смертоносні ходи, інформаційні війни та складні партії на кількох гравців — спроба знайти відповідь на питання: що творить нашу долю — воля людини чи обставини?
___

****
>[!quote] Цитата

****
>[!additional] Докладніше
>https://bit.ly/3HnrPNG

****

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