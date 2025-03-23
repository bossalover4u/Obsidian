---
type: book
author:
  - Лора Белоиван
titles: Far Eastern Shipping Company
series: 
cover: https://yakniga.org/_ipx/w_400,f_webp,fit_contain/https://yakniga.org/covers/books/29298/cover.jpg
start: 2022-08-01
end: 2022-08-06
status: done
---
![cover|200](Лора%20Белоиван%20-%20Far%20Eastern%20Shipping%20Company.webp)

Автор: [[Щоденник прочитаного/Автори/Лора Белоиван|Лора Белоиван]]
Название: `= this.titles`
Серия: `= this.series`
Номер в серии:
Основные персонажи:

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

dv.table(["Начал", "Закончил", "Продолжительность"], tableData);
```
---
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
>Один из разделов авторского сбоника "Маленькая хня"
Во-первых, в ней встречается ненормативная лексика! Во-вторых, изложение от первого лица, и это лицо- женское. При этом первое со вторым спрягаются изумительно, потому что органично. Отличная проза: смешная, интересная, с хорошо выраженным индивидуальным стилем.

> [!additional]- Зміст
> **Содержание:**
>
> - Ширинка
> - Какао, цветы и пианино
> - Угу
> - Инсекты
> - Дэбэ
> - Гирудотерапия
> - Замечания по работе
> - Сила искусства
> - Вектор прозрачности, или откуда берутся КДП
> - Пикус и др.)

---
- [[home|До бібліотеки]]
```dataviewjs
const currentFront = dv.current().file.frontmatter; // Получаем название текущей заметки
const year = parseInt(currentFront['end'].split('-')[0]); // Преобразуем название заметки (год) в число
const yearLink = dv.fileLink(`Щоденник прочитаного/Списки прочитаних книг по роках/${year}`, false, `Що я прочитав за ${year} рік`);
dv.list([yearLink]);
```